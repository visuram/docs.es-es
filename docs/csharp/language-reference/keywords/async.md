---
title: async (Referencia de C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- async_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- async keyword [C#]
- async method [C#]
- async [C#]
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
caps.latest.revision: 52
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: 8734f639e45f12ddd987a1c34e7f3ac38aa7d73f
ms.lasthandoff: 03/13/2017

---
# <a name="async-c-reference"></a>async (Referencia de C#)
Use el modificador `async` para especificar que un método, una [expresión lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) o un [método anónimo](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) es asincrónico. Si se utiliza este modificador en un método o una expresión, se hace referencia al mismo como método asincrónico.  
  
```csharp  
public async Task<int> ExampleMethodAsync()  
{  
    // . . . .  
}  
  
```  
  
 Si no está familiarizado con la programación asincrónica o no entiende cómo un método asincrónico usa la palabra clave `await` para hacer el trabajo de larga duración sin bloquear el subproceso del llamador, se recomienda leer la introducción de [Programación asincrónica con async y await](../../../csharp/programming-guide/concepts/async/index.md).  
  
```  
string contents = await contentsTask;  
```  
  
 El método se ejecuta sincrónicamente hasta alcanzar la primera expresión `await`, en la que se suspende el método hasta que se complete la tarea en espera. Mientras tanto, el control vuelve al llamador del método, como se muestra en el ejemplo de la sección siguiente.  
  
 Si el método que la palabra clave `async` modifica no contiene una expresión o instrucción `await`, el método se ejecuta de forma sincrónica. Una advertencia del compilador alerta de cualquier método asincrónico que no contenga `await`, porque esa situación podría indicar un error. Vea [Compiler Warning (level 1) CS4014](../../../csharp/language-reference/compiler-messages/cs4014.md) (Advertencia del compilador (nivel 1) CS4014).  
  
 La palabra clave `async` es contextual en el sentido de que es una palabra clave cuando modifica un método, una expresión lambda o un método anónimo. En todos los demás contextos, se interpreta como identificador.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra la estructura y el flujo de control entre un controlador de eventos asincrónicos, `StartButton_Click`, y un método asincrónico, `ExampleMethodAsync`. El resultado del método asincrónico es la longitud de un sitio web descargado. El código es adecuado para una aplicación Windows Presentation Foundation (WPF) o de la Tienda Windows creada en Visual Studio; vea los comentarios del código para configurar la aplicación.  
  
```csharp  
// You can run this code in Visual Studio 2013 as a WPF app or a Windows Store app.  
// You need a button (StartButton) and a textbox (ResultsTextBox).  
// Remember to set the names and handler so that you have something like this:  
// <Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"  
//         Click="StartButton_Click" Name="StartButton"/>  
// <TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"   
//          Text="TextBox" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>  
  
// To run the code as a WPF app:  
//    paste this code into the MainWindow class in MainWindow.xaml.cs,  
//    add a reference to System.Net.Http, and  
//    add a using directive for System.Net.Http.  
  
// To run the code as a Windows Store app:  
//    paste this code into the MainPage class in MainPage.xaml.cs, and  
//    add using directives for System.Net.Http and System.Threading.Tasks.  
  
private async void StartButton_Click(object sender, RoutedEventArgs e)  
{  
    // ExampleMethodAsync returns a Task<int>, which means that the method  
    // eventually produces an int result. However, ExampleMethodAsync returns  
    // the Task<int> value as soon as it reaches an await.  
    ResultsTextBox.Text += "\n";  
    try  
    {  
        int length = await ExampleMethodAsync();  
        // Note that you could put "await ExampleMethodAsync()" in the next line where  
        // "length" is, but due to when '+=' fetches the value of ResultsTextBox, you  
        // would not see the global side effect of ExampleMethodAsync setting the text.  
        ResultsTextBox.Text += String.Format("Length: {0}\n", length);  
    }  
    catch (Exception)  
    {  
        // Process the exception if one occurs.  
    }  
}  
  
public async Task<int> ExampleMethodAsync()  
{  
    var httpClient = new HttpClient();  
    int exampleInt = (await httpClient.GetStringAsync("http://msdn.microsoft.com")).Length;  
    ResultsTextBox.Text += "Preparing to finish ExampleMethodAsync.\n";  
    // After the following return statement, any method that's awaiting  
    // ExampleMethodAsync (in this case, StartButton_Click) can get the   
    // integer result.  
    return exampleInt;  
}  
// Output:  
// Preparing to finish ExampleMethodAsync.  
// Length: 53292  
  
```  
  
> [!IMPORTANT]
>  Para más información sobre las tareas y el código que se ejecuta mientras se espera la finalización por una tarea, vea [Programación asincrónica con async y await](../../../csharp/programming-guide/concepts/async/index.md). Para obtener un ejemplo completo de WPF que usa elementos similares, vea [Walkthrough: Accessing the Web by Using Async and Await](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) (Tutorial: obtener acceso a la web con Async y Await). Puede descargar el código del tutorial en [Ejemplos de código para desarrolladores](http://go.microsoft.com/fwlink/?LinkId=255191).  
  
## <a name="return-types"></a>Tipos de valor devueltos  
 El tipo de valor devuelto de un método asincrónico puede ser <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601> o [void](../../../csharp/language-reference/keywords/void.md). El método no puede declarar ningún parámetro [ref](../../../csharp/language-reference/keywords/ref.md) u [out](../../../csharp/language-reference/keywords/out.md), pero puede llamar a los métodos que tienen estos parámetros.  
  
 Se puede especificar `Task<TResult>` como el tipo de valor devuelto de un método asincrónico si la instrucción [return](../../../csharp/language-reference/keywords/return.md) del método especifica un operando de tipo `TResult`. Utilice `Task` si no se devuelve ningún valor significativo al completarse el método. Es decir, una llamada al método devuelve `Task`, pero cuando se completa `Task`, las expresiones `await` que esperan a que `Task` finalice se evalúan como `void`.  
  
 El tipo devuelto `void` se utiliza principalmente para definir controladores de eventos, que requieren ese tipo devuelto. El llamador de un método asincrónico que devuelva `void` no puede esperar a que finalice y no puede detectar las excepciones que el método inicia.  
  
 Para más información y ejemplos, vea [Tipos de valor devueltos asincrónicos](../../../csharp/programming-guide/concepts/async/async-return-types.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>   
 [await](../../../csharp/language-reference/keywords/await.md)   
 [Walkthrough: Accessing the Web by Using Async and Await](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)  (Tutorial: Acceso a la web con Async y Await)  
 [Programación asincrónica con Async y Await](../../../csharp/programming-guide/concepts/async/index.md)
