---
title: "Azure 存储帐户列表"
description: "使用 Azure Toolkit for Eclipse 管理存储帐户设置"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2016
ms.author: robmcm
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 91490e33ab2d524da90ae75bd71abe8005e45c54


---
# <a name="azure-storage-account-list"></a>Azure 存储帐户列表
使用 Azure 存储帐户，你可以针对 JDK、应用程序服务器和任意组件启用下载位置，并可以在使用缓存时用于存储状态。 Eclipse 维护了可供 Eclipse 工作区中的项目使用的已知存储帐户列表。 若要打开用于管理该列表的“存储帐户”对话框，请在 Eclipse 中单击“窗口”，单击“首选项”，展开“Azure”，然后单击“存储帐户”。

下面显示了“存储帐户”对话框。

![][ic719496]

也可以从使用存储帐户的对话框中的“帐户”链接打开此对话框，如下所示：

* “服务器配置”对话框的“JDK”选项卡。
* “服务器配置”对话框的“服务器”选项卡。
* “添加组件”对话框。
* “缓存”属性对话框。

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>使用发布设置文件导入存储帐户
1. 在“存储帐户”对话框中，单击“从发布设置文件导入”。
2. （如果你已到本地计算机上保存了发布设置文件，请跳过此步骤。）在“导入订阅信息”对话框中，单击“下载发布设置文件”。 如果你尚未登录到 Azure 帐户，则系统将提示你登录。 然后系统将提示你保存 Azure 发布设置文件。 （你可以忽略登录页中显示的最终说明 - 它们是由 Azure 门户提供的，适用于 Visual Studio 用户。）请将该文件保存到本地计算机。
3. 仍在“导入订阅信息”对话框中，单击“浏览”按钮，选择在前面保存到本地的发布设置文件，然后单击“打开”。
4. 单击“确定”关闭“导入订阅信息”对话框。

## <a name="to-create-a-new-storage-account"></a>新建新的存储帐户
1. 在“存储帐户”对话框中，单击“添加”。
2. 在“添加存储帐户”对话框中，单击“新建”。
3. 在“新建存储帐户”对话框中，指定以下设置的值：
   * 存储帐户名称。
   * 存储帐户的位置。
   * 存储帐户的说明。
   * 存储帐户所属的订阅。
4. 单击“确定”关闭“新建存储帐户”对话框。

创建存储帐户可能需要几分钟时间。 创建后，请单击“确定”关闭“添加存储帐户”对话框，新的存储帐户将添加到可用存储帐户列表中。

## <a name="to-add-an-existing-storage-account-to-the-list"></a>将现有存储帐户添加到列表
1. 如果没有 Azure 存储帐户，可以遵照上面“创建新的存储帐户”部分中列出的步骤创建一个存储帐户。 （或者，也可以在 [Azure 管理门户][Azure 管理门户]中创建新的存储帐户。）
2. 在“存储帐户”对话框中，单击“添加”。
3. 在“添加存储帐户”对话框中，输入“名称”和“访问密钥”的值。 这必须是现有 Azure 存储帐户的帐户名称和访问密钥。 可通过 [Azure 管理门户][Azure 管理门户]的“存储”部分查看存储帐户名称和密钥。 “添加存储帐户”对话框如下所示。
   
    ![][ic719497]
4. 单击“确定”关闭“添加存储帐户”对话框。

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>修改存储帐户以使用新的访问密钥
1. 在“存储帐户”对话框中，单击要编辑的存储帐户，然后单击“编辑”。
2. 在“编辑存储帐户访问密钥”对话框中，修改“访问密钥”值。
3. 单击“确定”关闭“编辑存储帐户访问密钥”对话框。

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>从 Eclipse 维护的列表中删除存储帐户
1. 在“存储帐户”对话框中，单击要编辑的存储帐户，然后单击“删除”。
2. 当系统提示是否删除该存储帐户时，单击“确定”。

> [!NOTE]
> 通过“存储帐户”对话框删除存储帐户只会从 Eclipse 中可查看的存储帐户列表中删除它， 而不会从 Azure 订阅中删除该存储帐户。 此外，在 Eclipse 重新加载订阅详细信息后，该存储帐户可能会再次出现在列表中。
> 
> 

## <a name="see-also"></a>另请参阅
[用于 Eclipse 的 Azure 工具包][用于 Eclipse 的 Azure 工具包]

[安装用于 Eclipse 的 Azure 工具包][安装用于 Eclipse 的 Azure 工具包] 

[在 Eclipse 中为 Azure 创建 Hello World 应用程序][在 Eclipse 中为 Azure 创建 Hello World 应用程序]

有关将 Azure 与 Java 配合使用的详细信息，请参阅 [Azure Java 开发人员中心][Azure Java 开发人员中心]。

<!-- URL List -->

[Azure Java 开发人员中心]: http://go.microsoft.com/fwlink/?LinkID=699547
[用于 Eclipse 的 Azure 工具包]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure 管理门户]: http://go.microsoft.com/fwlink/?LinkID=512959
[在 Eclipse 中为 Azure 创建 Hello World 应用程序]: http://go.microsoft.com/fwlink/?LinkID=699533
[安装用于 Eclipse 的 Azure 工具包]: http://go.microsoft.com/fwlink/?LinkId=699546
[用于 Eclipse 的 Azure 工具包的新增功能]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->



<!--HONumber=Nov16_HO3-->

