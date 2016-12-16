---
title: "Trabajar con registros de aplicaciones en Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "registros, aplicación"
  - "registros de eventos de aplicación, Visual Basic"
  - "registros de eventos de aplicación"
ms.assetid: 2581afd1-5791-4bc4-86b2-46244e9fe468
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Trabajar con registros de aplicaciones en Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Los objetos `My.Applicaton.Log` y `My.Log` facilitan la escritura de información de registro y seguimiento en los registros.  
  
## Cómo se registran los mensajes  
 En primer lugar, se comprueba la gravedad del mensaje con la propiedad <xref:System.Diagnostics.TraceSource.Switch%2A> de la propiedad <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A> del registro. De forma predeterminada, solo los mensajes de gravedad "Información" y superior se pasan a los agentes de escucha de seguimiento especificados en la colección `TraceListener` del registro. A continuación, cada agente de escucha compara la gravedad del mensaje con la propiedad <xref:System.Diagnostics.TraceSource.Switch%2A> del agente de escucha. Si la gravedad del mensaje es bastante alta, el agente de escucha escribe el mensaje.  
  
 En el siguiente diagrama se muestra cómo un mensaje escrito en el método `WriteEntry` se pasa a los métodos `WriteLine` de lo agentes de escucha de seguimiento del registro:  
  
 ![Llamada My Log](../../../../visual-basic/developing-apps/programming/log-info/media/mylogcall.png "MyLogCall")  
  
 Puede cambiar el archivo de configuración de la aplicación para modificar el comportamiento de los agentes de escucha de registro y de seguimiento. En el diagrama siguiente se muestra la correspondencia entre las partes del registro y el archivo de configuración.  
  
 ![Configuración de My Log](../../../../visual-basic/developing-apps/programming/log-info/media/mylogconfig.png "MyLogConfig")  
  
## Dónde se registran los mensajes  
 Si el ensamblado no tiene ningún archivo de configuración, los objetos `My.Application.Log` y `My.Log` escriben en la salida de depuración de la aplicación \(a través de la clase <xref:System.Diagnostics.DefaultTraceListener>\). Además, el objeto `My.Application.Log` escribe en el archivo de registro del ensamblado \(a través de la clase <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>\), mientras que el objeto `My.Log` escribe en la salida de la página web ASP.NET \(a través de la clase <xref:System.Web.WebPageTraceListener>\).  
  
 La salida de depuración se puede ver en la ventana **Salida** de [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] cuando la aplicación se ejecuta en modo de depuración. Para abrir la ventana **Salida**, haga clic en el elemento de menú **Depurar**, seleccione **Windows**, y, después, haga clic en **Salida**. En la ventana **Salida**, seleccione **Depurar** desde el cuadro **Mostrar resultados desde**.  
  
 De forma predeterminada, `My.Application.Log` escribe el archivo de registro en la ruta de acceso de los datos de aplicaciones del usuario. Puede obtener la ruta de acceso de la propiedad <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.FullLogFileName%2A> del objeto <xref:Microsoft.VisualBasic.Logging.Log.DefaultFileLogWriter%2A>. El formato de la ruta de acceso es el siguiente:  
  
 `BasePath`\\`CompanyName`\\`ProductName`\\`ProductVersion`  
  
 A continuación se indica un valor típico de `BasePath`.  
  
 C:\\Documents and Settings\\`username`\\Application Data  
  
 Los valores de `CompanyName`, `ProductName` y `ProductVersion` proceden de la información de ensamblado de la aplicación. El formato del nombre de archivo de registro es *nombreDeEnsamblado*.log, donde *nombreDeEnsamblado* es el nombre de archivo del ensamblado sin la extensión. Si se necesita más de un archivo de registro, por ejemplo, si el registro original no está disponible cuando la aplicación intenta escribir en el registro, el formato del nombre de archivo de registro es *nombreDeEnsamblado*\-*iteration*.log, donde `iteration` es un `Integer` positivo.  
  
 Para invalidar el comportamiento predeterminado, puede agregar o cambiar los archivos de configuración del equipo y de la aplicación. Para obtener más información, consulta [Tutorial: Cambiar el lugar donde My.Application.Log escribe información](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md).  
  
## Configurar el registro  
 El objeto `Log` tiene una implementación predeterminada que funciona sin un archivo de configuración de la aplicación, app.config. Para cambiar los valores predeterminados, debe agregar un archivo de configuración con la nueva configuración. Para obtener más información, consulta [Tutorial: Filtrar el resultado de My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md).  
  
 Las secciones de configuración de registro se encuentran en el nodo `<system.diagnostics>` del nodo principal `<configuration>` del archivo app.config. La información de registro se define en varios nodos:  
  
-   Los agentes de escucha del objeto `Log` se definen en el nodo `<sources>` denominado DefaultSource.  
  
-   El filtro de gravedad del objeto `Log` se definen en el nodo `<switches>` denominado DefaultSwitch.  
  
-   Los agentes de escucha de registro se definen en el nodo `<sharedListeners>`.  
  
 En el código siguiente, se muestran ejemplos de los nodos `<sources>`, `<switches>` y `<sharedListeners>`:  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="DefaultSource" switchName="DefaultSwitch">  
        <listeners>  
          <add name="FileLog"/>  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="DefaultSwitch" value="Information" />  
    </switches>  
    <sharedListeners>  
      <add name="FileLog"  
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,  
          Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,   
          PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL"  
        initializeData="FileLogWriter"  
      />  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## Cambiar la configuración de registro después de la implementación  
 Al desarrollar una aplicación, su configuración se almacena en el archivo app.config, tal como se muestra en los ejemplos anteriores. Después de implementar su aplicación, puede configurar el registro mediante la edición del archivo de configuración. En una aplicación basada en Windows, el nombre de este archivo es *nombreDeAplicación*.exe.config y debe encontrarse en la misma carpeta que el archivo ejecutable. En una aplicación web, es el archivo Web.config asociado al proyecto.  
  
 Cuando la aplicación ejecuta el código que crea una instancia de una clase por primera vez, comprueba el archivo de configuración para obtener información sobre el objeto. En el caso del objeto `Log`, estos sucede la primera vez que se accede al objeto `Log`. El sistema examina el archivo de configuración una sola vez par cada objeto concreto \(la primera vez que la aplicación crea el objeto\). Por lo tanto, es posible que deba reiniciar la aplicación para que los cambios surtan efecto.  
  
 En una aplicación implementada, el código de seguimiento se habilita volviendo a configurar los objetos modificadores antes de que se inicie la aplicación. Normalmente, esto implica activar y desactivar los objetos modificadores. Para ello, se deben cambiar los niveles de seguimiento y, luego, reiniciar la aplicación.  
  
## Consideraciones de seguridad  
 Tenga en cuenta lo siguiente al escribir datos en el registro:  
  
-   **Evite la pérdida de información de usuario.** Asegúrese de que la aplicación solo escribe información aprobada en el registro. Por ejemplo, es posible que se acepte que el registro de la aplicación contenga nombres de usuario, pero no contraseñas de usuario.  
  
-   **Proteja las ubicaciones del registro.** Cualquier registro que contenga información que pueda ser confidencial debe almacenarse en una ubicación segura.  
  
-   **Evite información engañosa.** En general, la aplicación debe validar todos los datos introducidos por un usuario antes de usarlos. Se incluye la escritura de datos en el registro de la aplicación.  
  
-   **Evite la denegación de servicio.** Si su aplicación escribe demasiada información en el registro, podría llenar el registro o dificultar la búsqueda de información importante.  
  
## Vea también  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Registrar información de la aplicación](../../../../visual-basic/developing-apps/programming/log-info/logging-information-from-the-application.md)