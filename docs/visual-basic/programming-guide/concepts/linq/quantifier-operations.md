---
title: 限定符操作 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: ae1a2b73-503c-4f4b-a3fd-31b5adbee67c
ms.openlocfilehash: 0a0a5fae35a14ab6451f2f56fb2eedd92ac437e7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33645825"
---
# <a name="quantifier-operations-visual-basic"></a>限定符操作 (Visual Basic)
限定符运算返回一个 <xref:System.Boolean> 值，该值指示序列中是否有一些元素满足条件或是否所有元素都满足条件。  
  
 下图描述了两个不同源序列上的两个不同限定符运算。 第一个运算询问是否有一个或多个元素为字符“A”，结果为 `true`。 第二个运算询问是否所有元素都为字符“A”，结果为 `true`。  
  
 ![LINQ 限定符运算](../../../../csharp/programming-guide/concepts/linq/media/linq_quantifier.png "LINQ_Quantifier")  
  
 下节列出了执行限定符运算的标准查询运算符方法。  
  
## <a name="methods"></a>方法  
  
|方法名|描述|Visual Basic 查询表达式语法|详细信息|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|全部|确定是否序列中的所有元素都满足条件。|`Aggregate … In … Into All(…)`|<xref:System.Linq.Enumerable.All%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.All%2A?displayProperty=nameWithType>|  
|任意|确定序列中是否有元素满足条件。|`Aggregate … In … Into Any()`|<xref:System.Linq.Enumerable.Any%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Any%2A?displayProperty=nameWithType>|  
|包含|确定序列是否包含指定的元素。|不适用。|<xref:System.Linq.Enumerable.Contains%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Contains%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>查询表达式语法示例  
 这些示例使用`Aggregate`作为 LINQ 查询中的筛选条件的一部分的 Visual Basic 中的子句。  
  
 下面的示例使用`Aggregate`子句和<xref:System.Linq.Enumerable.All%2A>扩展方法以从集合中返回其宠物是所有早于指定的期限那些人。  
  
 [!code-vb[CsLINQAnyAll#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/quantifier-operations_1.vb)]  
  
 下一个示例使用`Aggregate`子句和<xref:System.Linq.Enumerable.Any%2A>扩展方法以从集合返回至少具有一个那些人只宠物的是早于指定的期限。  
  
 [!code-vb[CsLINQAnyAll#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/quantifier-operations_2.vb)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Linq>  
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)  
 [Aggregate 子句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)  
 [如何： 查询包含一组指定的单词 (LINQ) (Visual Basic) 的句子](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)
