---
title: 使用准则
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], usage guidelines
ms.assetid: 42215ffa-a099-4a26-b14e-fb2bdb6f95b7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 04e44a6b58fd334b6a23e113922b980f69de627b
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2018
ms.locfileid: "44198642"
---
# <a name="usage-guidelines"></a>使用准则

本部分包含在可公开访问的 Api 中使用公共类型的指导原则。 它可以处理直接使用内置的框架类型 （例如，序列化属性） 和重载常见的运算符。
  
<xref:System.IDisposable?displayProperty=nameWithType>接口未涵盖在此部分中，但在讨论[Dispose 模式](../../../docs/standard/design-guidelines/dispose-pattern.md)部分。

> [!NOTE]
> 有关指导原则和其他常见有关其他信息，内置的.NET Framework 类型，请参阅以下参考主题： <xref:System.DateTime?displayProperty=nameWithType>， <xref:System.DateTimeOffset?displayProperty=nameWithType>， <xref:System.ICloneable?displayProperty=nameWithType>， <xref:System.IComparable%601?displayProperty=nameWithType>， <xref:System.IEquatable%601?displayProperty=nameWithType>， <xref:System.Nullable%601?displayProperty=nameWithType>， <xref:System.Object?displayProperty=nameWithType>, <xref:System.Uri?displayProperty=nameWithType>.

## <a name="in-this-section"></a>本节内容

[数组](arrays.md)  
[特性](attributes.md)  
[集合](guidelines-for-collections.md)  
[序列化](serialization.md)  
[System.Xml 使用情况](system-xml-usage.md)  
[相等运算符](equality-operators.md)  

*部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*

*经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第2版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
