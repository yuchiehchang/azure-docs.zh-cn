---
title: "安装应用程序访问面板浏览器扩展时遇到问题 | Microsoft Docs"
description: "如何修复安装访问面板浏览器扩展时遇到的常见错误"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
translationtype: Human Translation
ms.sourcegitcommit: 0d6f6fb24f1f01d703104f925dcd03ee1ff46062
ms.openlocfilehash: 40ace51c4ba74039b3a5d5997acdf2da7b98b4a9
ms.lasthandoff: 04/18/2017


---

# <a name="problem-installing-the-application-access-panel-browser-extension"></a>安装应用程序访问面板浏览器扩展时遇到问题

访问面板是一个基于 Web 的门户，在 Azure Active Directory (Azure AD) 中拥有工作或学校帐户的用户可以使用它来查看和启动 Azure AD 管理员已授权他们访问的基于云的应用程序。 拥有 Azure AD 版本的用户还可以通过访问面板使用自助组和应用管理功能。 访问面板不同于 Azure 门户，它不要求用户拥有 Azure 订阅。

若要在访问面板中使用基于密码的单一登录 (SSO)，必须在用户的浏览器中安装访问面板扩展。 当用户选择某个已配置基于密码的 SSO 的应用程序时，会自动下载此扩展。

## <a name="meeting-browser-requirements-for-the-access-panel"></a>满足访问面板对浏览器的要求

访问面板要求浏览器支持 JavaScript 且已启用 CSS。 若要在访问面板中使用基于密码的单一登录 (SSO)，必须在用户的浏览器中安装访问面板扩展。 当用户选择某个已配置基于密码的 SSO 的应用程序时，会自动下载此扩展。

对于基于密码的 SSO，最终用户的浏览器可以是：

-   Internet Explorer 8、9、10、11 - 在 Windows 7 或更高版本上

-   Chrome -- 在 Windows 7 或更高版本上，以及在 MacOS X 或更高版本上

-   Firefox 26.0 或更高版本 -- 在 Windows XP SP2 或更高版本上，以及在 Mac OS X 10.6 或更高版本上

**注意：**当 Edge 开始支持浏览器扩展时，基于密码的 SSO 扩展将可供 Windows 10 中的 Edge 使用。

## <a name="how-to-install-the-access-panel-browser-extension"></a>如何安装访问面板浏览器扩展

若要安装访问面板浏览器扩展，请执行以下步骤：

1.  在任一支持的浏览器中打开“访问面板”[](https://myapps.microsoft.com)，并以 Azure AD 中的**用户**身份登录。

2.  在访问面板中单击“密码-SSO 应用程序”。

3.  在询问是否安装软件的提示消息中，选择“立即安装”。

4.  基于浏览器，系统将定向到下载链接。 将扩展**添加**到浏览器中。

5.  如果浏览器出现提示，选择“启用”或“允许”扩展。

6.  安装完成后，**重启**浏览器会话。

7.  登录访问面板，查看是否可以**启动**密码-SSO 应用程序

也可以使用下面的直接链接下载适用于 Chrome 和 Firefox 的扩展：

-   [Chrome 访问面板扩展](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox 访问面板扩展](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>设置 Internet Explorer 的组策略

通过设置组策略，可在用户的计算机上远程安装 Internet Explorer 的访问面板扩展。

先决条件包括：

-   已设置 [Active Directory 域服务](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)，并且已将用户的计算机加入你的域。

-   必须拥有“编辑设置”权限才能编辑组策略对象 (GPO)。 默认情况下，以下安全组的成员拥有此权限：域管理员、企业管理员和组策略创建者和所有者。 [了解详细信息](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)。

有关如何配置组策略以及将其部署给用户的分步说明，请参阅教程[如何使用组策略部署 Internet Explorer 的访问面板扩展](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy)。

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a>对 Internet Explorer 中的访问面板进行故障排除

若要访问诊断工具以及获得为 IE 配置扩展的分步说明，请按照[对 Internet Explorer 的访问面板进行故障排除](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot)指南进行操作。

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a>如果这些故障排除步骤未解决此问题

请打开支持票证，并提供以下信息（如有）：

-   相关错误 ID

-   UPN（用户电子邮件地址）

-   TenantID

-   浏览器类型

-   错误出现的时区和时间/时间段

-   Fiddler 跟踪

## <a name="next-steps"></a>后续步骤
[Azure Active Directory 的应用程序访问与单一登录是什么？](active-directory-appssoaccess-whatis.md)
