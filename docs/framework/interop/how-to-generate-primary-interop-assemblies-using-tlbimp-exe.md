---
title: "如何：使用 Tlbimp.exe 生成主互操作程序集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "主互操作程序集, 生成"
  - "Tlbimp.exe"
  - "类型库导入程序"
ms.assetid: 5419011c-6e57-40f6-8c65-386db8f7a651
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用 Tlbimp.exe 生成主互操作程序集
有两种生成主互操作程序集的方法：  
  
-   使用由 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 提供的[类型库导入程序 \(Tlbimp.exe\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)。  
  
     生成主互操作程序集的最简单方法是使用 [Tlbimp.exe（类型库导入程序）](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)。  Tlbimp.exe 提供了以下安全措施：  
  
    -   在为任何嵌套的类型库引用创建新的互操作程序集之前，检查其他已注册的主互操作程序集。  
  
    -   如果未指定容器或文件名称赋予主互操作程序集文件强名称，则将无法发出主互操作程序集。  
  
    -   如果省略对依赖程序集的引用，则无法发出主互操作程序集。  
  
    -   如果将引用添加到不是主互操作程序集的依赖程序集，则无法发出主互操作程序集。  
  
-   在源代码中使用符合公共语言规范 \(CLS\)（如 C\#）的语言手动创建主互操作程序集。  当类型库不可用时，此方法非常有用。  
  
 要使用强名称为程序集签名，必须具有加密密钥对。  有关详细信息，请参阅[创建密钥对](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)。  
  
### 若要使用 Tlbimp.exe 生成主互操作程序集  
  
1.  在命令提示符处，键入：  
  
     **tlbimp** *tlbfile*  **\/primary \/keyfile:** *filename* **\/out:** *assemblyname*  
  
     在此命令中，*tlbfile* 是要包含 COM 类型库的文件，*filename* 是包含密钥对的容器或文件的名称，*assemblyname* 是要使用强名称签名的程序集的名称。  
  
 主互操作程序集仅可引用其他主互操作程序集。  如果你的程序集从第三方 COM 类型库引用类型，则必须在生成主互操作程序集之前，先从发布服务器上获取主互操作程序集。  如果你是发布者，则必须在生成引用的主互操作程序集之前，生成依赖类型库的主互操作程序集。  
  
 当具有不同于原始类型库的版本号的依赖主互操作程序集安装在当前目录时，此程序集是不可发现的。  必须在 Windows 注册表中注册此依赖主互操作程序集，或者使用 **\/reference** 选项确保 Tlbimp.exe 可以找到依赖 DLL。  
  
 还可以包装类型库的多个版本。  有关说明，请参阅[How to: Wrap Multiple Versions of Type Libraries](http://msdn.microsoft.com/zh-cn/79eefe04-a770-4bc3-8ea2-e90ddb8ec31f)。  
  
## 示例  
 以下示例导入 COM 类型库 `LibUtil.tlb` 并借助密钥文件 `CompanyA.snk` 为程序集 `LibUtil.dll` 签署强名称。  通过省略特定的命名空间名称，此示例将生成默认的命名空间，`LibUtil`。  
  
```  
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /out:LibUtil.dll  
```  
  
 对于更具描述性的名称（使用 *VendorName*.*LibraryName* 命名规则），以下示例将重写默认程序集的文件名和命名空间名称。  
  
```  
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /namespace:CompanyA.LibUtil /out:CompanyA.LibUtil.dll  
```  
  
 以下示例导入引用 `CompanyA.LibUtil.dll` 的 `MyLib.tlb`，并借助密钥文件 `CompanyB.snk` 为程序集 `CompanyB.MyLib.dll` 签署强名称。  命名空间 `CompanyB.MyLib` 将重写默认的命名空间名称。  
  
```  
tlbimp MyLib.tlb /primary /keyfile:CompanyB.snk /namespace:CompanyB.MyLib /reference:CompanyA.LibUtil.dll /out:CompanyB.MyLib.dll  
```  
  
## 请参阅  
 [如何：注册主互操作程序集](../../../docs/framework/interop/how-to-register-primary-interop-assemblies.md)