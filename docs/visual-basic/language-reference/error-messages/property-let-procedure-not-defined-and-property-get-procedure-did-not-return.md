---
title: "El procedimiento Let de la propiedad no est&#225; definido y el procedimiento Get no ha devuelto un objeto | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID451"
dev_langs: 
  - "VB"
ms.assetid: 8542382a-689f-4e1b-abc0-c1e2dadb92f4
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# El procedimiento Let de la propiedad no est&#225; definido y el procedimiento Get no ha devuelto un objeto
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Determinadas propiedades, métodos y operaciones sólo se pueden aplicar a objetos `Collection`.  Ha especificado una operación o propiedad que es exclusiva para colecciones, pero el objeto no es una colección.  
  
### Para corregir este error  
  
1.  Compruebe que ha escrito correctamente el nombre de objeto o propiedad, o compruebe que el objeto es de tipo `Collection`.  
  
2.  Busque el método `Add` utilizado para agregar el objeto a la colección a fin de asegurarse de que la sintaxis es correcta y de que ha escrito correctamente los identificadores.  
  
## Vea también  
 <xref:Microsoft.VisualBasic.Collection>