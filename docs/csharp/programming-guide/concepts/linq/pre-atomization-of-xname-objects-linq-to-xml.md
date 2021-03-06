---
title: "Atomización previa de objetos XName (LINQ to XML) (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: e84fbbe7-f072-4771-bfbb-059d18e1ad15
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f2e324029a4951f1cb05507d580db73caea2d3f7
ms.lasthandoff: 03/13/2017


---
# <a name="pre-atomization-of-xname-objects-linq-to-xml-c"></a>Atomización previa de objetos XName (LINQ to XML) (C#)
Una manera de mejorar el rendimiento en LINQ to XML es realizar una atomización previa de los objetos <xref:System.Xml.Linq.XName>. Atomización previa significa que asigna una cadena a un objeto <xref:System.Xml.Linq.XName> antes de que cree el árbol XML mediante los constructores de las clases <xref:System.Xml.Linq.XElement> y <xref:System.Xml.Linq.XAttribute>. Después, en lugar de pasar una cadena al constructor, que usaría la conversión implícita de cadena a <xref:System.Xml.Linq.XName>, pase el objeto <xref:System.Xml.Linq.XName> inicializado.  
  
 Esto mejora el rendimiento si crear un árbol XML de gran tamaño en el que se repiten nombres específicos. Para ello, debe declarar e inicializar los objetos <xref:System.Xml.Linq.XName> antes de construir el árbol XML y, después, usar los objetos <xref:System.Xml.Linq.XName> en lugar de especificar las cadenas para los nombres de atributo y elemento. Esta técnica puede producir un aumento significativo del rendimiento si va a crear un gran número de elementos (o atributos) con el mismo nombre.  
  
 Debería probar la atomización previa con su situación para decidir si debe utilizarla.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo hacerlo.  
  
```csharp  
XName Root = "Root";  
XName Data = "Data";  
XName ID = "ID";  
  
XElement root = new XElement(Root,  
    new XElement(Data,  
        new XAttribute(ID, "1"),  
        "4,100,000"),  
    new XElement(Data,  
        new XAttribute(ID, "2"),  
        "3,700,000"),  
    new XElement(Data,  
        new XAttribute(ID, "3"),  
        "1,150,000")  
);  
  
Console.WriteLine(root);  
```  
  
 Este ejemplo produce el siguiente resultado:  
  
```xml  
<Root>  
  <Data ID="1">4,100,000</Data>  
  <Data ID="2">3,700,000</Data>  
  <Data ID="3">1,150,000</Data>  
</Root>  
```  
  
 En el siguiente ejemplo se muestra la misma técnica donde el documento XML se encuentra en un espacio de nombres:  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XName Root = aw + "Root";  
XName Data = aw + "Data";  
XName ID = "ID";  
  
XElement root = new XElement(Root,  
    new XAttribute(XNamespace.Xmlns + "aw", aw),  
    new XElement(Data,  
        new XAttribute(ID, "1"),  
        "4,100,000"),  
    new XElement(Data,  
        new XAttribute(ID, "2"),  
        "3,700,000"),  
    new XElement(Data,  
        new XAttribute(ID, "3"),  
        "1,150,000")  
);  
  
Console.WriteLine(root);  
```  
  
 Este ejemplo produce el siguiente resultado:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Data ID="1">4,100,000</aw:Data>  
  <aw:Data ID="2">3,700,000</aw:Data>  
  <aw:Data ID="3">1,150,000</aw:Data>  
</aw:Root>  
```  
  
 El ejemplo siguiente es más similar a lo que probablemente encontrará en el mundo real. En este ejemplo, una consulta proporciona el contenido del elemento:  
  
```csharp  
XName Root = "Root";  
XName Data = "Data";  
XName ID = "ID";  
  
DateTime t1 = DateTime.Now;  
XElement root = new XElement(Root,  
    from i in System.Linq.Enumerable.Range(1, 100000)  
    select new XElement(Data,  
        new XAttribute(ID, i),  
        i * 5)  
);  
DateTime t2 = DateTime.Now;  
  
Console.WriteLine("Time to construct:{0}", t2 - t1);  
```  
  
 El ejemplo anterior se ejecuta mejor que el siguiente, en el que los nombres no se atomizan previamente:  
  
```csharp  
DateTime t1 = DateTime.Now;  
XElement root = new XElement("Root",  
    from i in System.Linq.Enumerable.Range(1, 100000)  
    select new XElement("Data",  
        new XAttribute("ID", i),  
        i * 5)  
);  
DateTime t2 = DateTime.Now;  
  
Console.WriteLine("Time to construct:{0}", t2 - t1);  
```  
  
## <a name="see-also"></a>Vea también  
 [Rendimiento (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/performance-linq-to-xml.md)   
 [Objetos XName y XNamespace atomizados (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/atomized-xname-and-xnamespace-objects-linq-to-xml.md)
