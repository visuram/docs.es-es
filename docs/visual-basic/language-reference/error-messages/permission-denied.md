---
title: "Permiso denegado (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID70"
dev_langs: 
  - "VB"
ms.assetid: 71f46756-f522-4814-aab4-492bf9924245
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Permiso denegado (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se ha intentado escribir en un disco protegido contra escritura u obtener acceso a una archivo bloqueado.  
  
### Para corregir este error  
  
1.  Para abrir un archivo protegido contra escritura, cambie el atributo de protección contra escritura del archivo.  
  
2.  Asegúrese de que otro proceso no ha bloqueado el archivo y espere a abrir el archivo hasta que el otro proceso lo libere.  
  
3.  Para tener acceso al Registro, compruebe que sus permisos de usuario incluyen este tipo de acceso al Registro.  
  
## Vea también  
 [Tipos de error](../../../visual-basic/programming-guide/language-features/error-types.md)