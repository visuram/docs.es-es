---
title: Leer y escribir en el Registro (Visual Basic) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My.Computer.Registry object, tasks
- registry, writing to
- registry, reading
ms.assetid: a13da106-185b-41d7-b23c-416da65e21e4
caps.latest.revision: 21
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1f148b00181c6c6a152b2f08ab765e0a385a7c89
ms.lasthandoff: 03/13/2017

---
# <a name="reading-from-and-writing-to-the-registry-visual-basic"></a>Leer y escribir en el Registro (Visual Basic)
En este tema se describen las tareas y los temas conceptuales asociados al Registro.  
  
 Al programar en [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], puede tener acceso al Registro mediante las funciones proporcionadas por [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] o mediante las clases de Registro de .NET Framework. El Registro hospeda información del sistema operativo, así como de las aplicaciones hospedadas en el equipo. Si trabaja con el Registro, puede poner en peligro la seguridad al permitir accesos inadecuados a recursos del sistema o a información protegida.  
  
## <a name="in-this-section"></a>En esta sección  
 [Crear una clave del Registro y establecer su valor](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-create-a-registry-key-and-set-its-value.md)  
 Describe cómo usar los métodos `CreateSubKey` y `SetValue` del objeto `My.Computer.Registry` para crear una clave del Registro y establecer su valor.  
  
 [Leer un valor a partir de una clave del Registro](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-read-a-value-from-a-registry-key.md)  
 Describe cómo usar el método `GetValue` del objeto `My.Computer.Registry` para leer un valor de una clave del Registro.  
  
 [Eliminar una clave del Registro](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-delete-a-registry-key.md)  
 Describe cómo usar el método `DeleteSubKey` de la propiedad `My.Computer.Registry.CurrentUser` para eliminar una clave del Registro.  
  
 [Leer y escribir en el Registro mediante Microsoft.Win32 Namespace](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry-using-the-microsoft-win32-namespace.md)  
 Describe cómo usar las clases `Registry` y `RegistryKey` de [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] para tener acceso al Registro.  
  
 [Seguridad y Registro](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)  
 Describe problemas de seguridad que afectan al Registro.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>  
 Enumera y explica los miembros del objeto `My.Computer.Registry`.  
  
 <xref:Microsoft.Win32.Registry>  
 Ofrece información general sobre la clase `Registry`, junto con vínculos a claves y miembros individuales.
