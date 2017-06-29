---
title: "Azure Analysis Services 教程第 3 课：标记为日期表 | Microsoft Docs"
description: "介绍了在 Azure Analysis Services 教程项目中如何标记日期表。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.translationtype: Human Translation
ms.sourcegitcommit: 43aab8d52e854636f7ea2ff3aae50d7827735cc7
ms.openlocfilehash: c62f2726fef5219155a08b70c61162c914600d1d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/03/2017

---
# <a name="lesson-3-mark-as-date-table"></a>第 3 课：标记为日期表

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在“第 2 课：获取数据”中，你已导入了一个名为 DimDate 的维度表。 虽然此表在你的模型中名为 DimDate，但它也称为日期表，因为其中包含日期和时间数据。  
  
每当使用 DAX 时间智能函数时（如稍后创建度量值时），必须指定属性，这包括日期表和该表中的唯一标识符日期列。
  
在本课中，你将把 DimDate 表标记为日期表，并把 Date 列（在日期表中）标记为日期列（唯一标识符）。  

在标记日期表和日期列之前，最好做一些保养工作以使你的模型更容易理解。 请注意“DimDate”表中名为“FullDateAlternateKey”的列。 此列包含的每一行表示表中每个日历年的每一天。 在度量值公式和报表中将大量使用此列。 但是，对于此列，FullDateAlternateKey 实际上不是一个很好的标识符。 将其重命名为“Date”，使其更容易识别以及包括在公式中。 只要有可能，最好对表和列之类的对象进行重命名以使其在 SSDT 和客户端报告应用程序（例如 Power BI 和 Excel）中更容易识别。 
  
本课预计完成时间：3 分钟  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课中的任务之前，你应当已完成上一课：[第 2 课：获取数据](../tutorials/aas-lesson-2-get-data.md)。 

### <a name="to-rename-the-fulldatealternatekey-column"></a>重命名 FullDateAlternateKey 列

1.  在模型设计器中，单击“DimDate”表。

2.  双击“FullDateAlternateKey”列的标题，然后将其重命名为“Date”。

  
### <a name="to-set-mark-as-date-table"></a>标记为日期表  
  
1.  选择“Date”列，然后在“属性”窗口中在“数据类型”下确保“Date”处于选中状态。  
  
2.  单击“表”菜单，然后依次单击“Date”和“标记为日期表”。  
  
3.  在“标记为日期表”对话框中，在“Date”列表框中，选择“Date”列作为唯一标识符。 它通常默认处于选中状态。 单击 **“确定”**。 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>后续步骤
[第 4 课：创建关系](../tutorials/aas-lesson-4-create-relationships.md)。
  
