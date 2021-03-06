---
title: 如何：在注册表中创建注册表项 (Visual C#)
ms.date: 07/20/2015
helpviewer_keywords:
- registry, adding keys and values [C#]
- registry keys, creating [C#]
- keys, creating in registry
ms.assetid: 8fa475b0-e01f-483a-9327-fd03488fdf5d
ms.openlocfilehash: 383d47413078359d7491bf5f7f61dc5e70d842a7
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43526733"
---
# <a name="how-to-create-a-key-in-the-registry-visual-c"></a>如何：在注册表中创建注册表项 (Visual C#)
本示例将值对“Name”和“Isabella”添加到当前用户注册表中的项“Names”之下。  
  
## <a name="example"></a>示例  
  
```csharp  
Microsoft.Win32.RegistryKey key;  
key = Microsoft.Win32.Registry.CurrentUser.CreateSubKey("Names");  
key.SetValue("Name", "Isabella");  
key.Close();  
```  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   复制代码，并将其粘贴到控制台应用程序的 `Main` 方法中。  
  
-   将 `Names` 参数替换为直接存在于注册表 HKEY_CURRENT_USER 节点下的项的名称。  
  
-   将 `Name` 参数替换为直接存在于“Names”节点下的值的名称。  
  
## <a name="robust-programming"></a>可靠编程  
 检查注册表结构，查找适合项的位置。 例如，可能需要打开当前用户的 Software 项，并用公司的名称创建一项。 然后将注册表值添加到公司的项上。  
  
 以下情况可能会导致异常：  
  
-   项的名称为空。  
  
-   用户没有创建注册表项的权限。  
  
-   项名称超过 255 个字符的限制。  
  
-   项已关闭。  
  
-   注册表项为只读。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 将数据写入用户文件夹 `Microsoft.Win32.Registry.CurrentUser` 比写入本地计算机 `Microsoft.Win32.Registry.LocalMachine` 更安全。  
  
 创建注册表值时，需要确定该值已存在时应执行的操作。 另一进程（可能是恶意进程）可能已创建了该值，并拥有对该值的访问权。 将数据放入注册表值后，其他进程即可使用这些数据。 若要防止出现这种情况，请使用 `Overload:Microsoft.Win32.RegistryKey.GetValue` 方法。 如果项不存在，则该方法返回 null。  
  
 即使注册表项受访问控制列表 (ACL) 保护，在注册表中以纯文本形式存储机密信息（例如密码）也不安全。  
  
## <a name="see-also"></a>请参阅

- <xref:System.IO?displayProperty=nameWithType>  
- [C# 编程指南](../../../csharp/programming-guide/index.md)  
- [文件系统和注册表（C# 编程指南）](../../../csharp/programming-guide/file-system/index.md)  
- [Read, write and delete from the registry with C#](http://www.codeproject.com/Articles/3389/Read-write-and-delete-from-registry-with-C)（使用 C# 在注册表中执行读取、写入和删除操作）
