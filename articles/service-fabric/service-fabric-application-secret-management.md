---
title: 管理 Azure Service Fabric 应用程序机密 | Microsoft Docs
description: 了解如何保护 Service Fabric 应用程序中的机密值。
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/21/2018
ms.author: vturecek
ms.openlocfilehash: fa79d50d6ef2899dcaf4116dcfe8ac7fae077959
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2018
---
# <a name="manage-secrets-in-service-fabric-applications"></a>管理 Service Fabric 应用程序中的机密
本指南逐步讲解管理 Service Fabric 应用程序中的机密的步骤。 机密可以是任何敏感信息，例如存储连接字符串、密码或其他不应以明文形式处理的值。

[Azure 密钥保管库][key-vault-get-started]在此处用作证书的安全存储位置，也可用于将证书安装在 Azure 中的 Service Fabric 群集上。 如果不部署到 Azure，则不需要使用密钥保管库来管理 Service Fabric 应用程序中的机密。 但是，在应用程序中*使用*机密的方式不区分云平台，因此可让应用程序部署到托管在任何位置的群集。 

## <a name="obtain-a-data-encipherment-certificate"></a>获取数据加密证书
数据加密证书只用于加密和解密服务 Settings.xml 中的配置值，而不用于身份验证或密码文本签名。 该证书必须满足以下要求：

* 证书必须包含私钥。
* 必须为密钥交换创建证书，并且该证书可导出到个人信息交换 (.pfx) 文件。
* 证书密钥用途必须包括数据加密 (10)，不应包括服务器身份验证或客户端身份验证。 
  
  例如，使用 PowerShell 创建自签名证书时，`KeyUsage` 标志必须设置为 `DataEncipherment`：
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a>在群集中安装证书
必须在群集中的每个节点上安装此证书。 在运行时，将使用此证书解密服务的 Settings.xml 中存储的值。 有关设置说明，请参阅[如何使用 Azure 资源管理器创建群集][service-fabric-cluster-creation-via-arm]。 

## <a name="encrypt-application-secrets"></a>加密应用程序机密
在部署应用程序时使用证书加密机密值，并将其注入服务的 Settings.xml 配置文件。 Service Fabric SDK 提供内置的机密加密和解密函数。 可以在生成时加密机密值，在服务代码中以编程方式解密和读取机密值。 

以下 PowerShell 命令用于加密机密。 此命令仅加密值；**不**对密码文本进行签名。 若要生成机密值的密文，必须使用群集中安装的同一个加密证书：

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

生成的 base-64 编码字符串包含机密密文，以及用来将其加密的证书相关信息。  当 `IsEncrypted` 属性设置为 `true` 时，可将 base-64 编码字符串插入服务 Settings.xml 配置文件中的参数内：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>将应用程序机密插入应用程序实例
理想情况下，部署到不同环境的过程应尽可能自动化。 这可以通过在生成环境中执行机密加密，并在创建应用程序实例时提供加密机密作为参数来实现。

#### <a name="use-overridable-parameters-in-settingsxml"></a>在 Settings.xml 中使用可重写参数
Settings.xml 配置文件允许使用可在创建应用程序时提供的可重写参数。 使用 `MustOverride` 属性而不要提供参数值：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

若要重写 Settings.xml 中的值，可在 ApplicationManifest.xml 中声明服务的 override 参数：

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

现在，可以在创建应用程序实例时会值指定为*应用程序参数*。 可以使用 PowerShell 或 C# 编写用于创建应用程序实例的脚本，方便在生成过程中轻松集成。

使用 PowerShell 时，参数以[哈希表](https://technet.microsoft.com/library/ee692803.aspx)的形式提供给 `New-ServiceFabricApplication`：

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

使用 C# 时，应用程序参数以 `NameValueCollection` 的形式在 `ApplicationDescription` 中指定：

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>解密服务代码中的机密
可通过将加密机密使用的加密证书用于解密，从 Settings.xml 中读取加密值。 在 Windows 上，Service Fabric 中的服务默认在“网络服务”下运行，如果未提供额外的设置，它们无权访问节点上安装的证书。

使用数据加密证书时，需确保“网络服务”或运行服务的任何用户帐户可以访问该证书的私钥。 如果提供了相应的配置，Service Fabric 可自动处理服务授权。 可以通过在 ApplicationManifest.xml 中定义用户和证书安全策略来完成此配置。 在以下示例中，已授予“网络服务”帐户对某个按指纹定义的证书的读取访问权限：

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> 在 Windows 上从证书存储管理单元中复制证书指纹时，会在证书指纹字符串的开头添加一个不可见的字符。 尝试按指纹查找证书时，此不可见字符可能导致出错，因此请务必删除这个附加字符。
> 
> 

### <a name="use-application-secrets-in-service-code"></a>在服务代码中使用应用程序机密
借助用于访问配置包中 Settings.xml 内的配置值的 API，可以轻松解密 `IsEncrypted` 属性设置为 `true` 的值。 由于加密的文本包含用于加密的证书相关信息，因此不需要手动查找证书。 只需在运行服务的节点上安装该证书。 调用 `DecryptValue()` 方法即可检索原始机密值：

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>后续步骤
深入了解[应用程序和服务安全性](service-fabric-application-and-service-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-and-service-manifests.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
