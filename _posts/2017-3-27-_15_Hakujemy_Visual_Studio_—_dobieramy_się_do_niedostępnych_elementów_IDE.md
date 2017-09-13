---
layout:     post
title:      Hakujemy Visual Studio — dobieramy się do niedostępnych elementów IDE
date:       2017-03-27 18:26:00
summary:    API udostępnione przez SDK do Visual Studio pozwala na olbrzymie zmiany w IDE. Niestety nie zawsze to co chcemy zrobić jest możliwe w oficjalny sposób. W tym wpisie przedstawię sposób na modyfikowanie elementów interfejsu Visual Studio, które nie są możliwe poprzez API. Będziemy hakowali Visuala :)A...
categories: windows oprogramowanie programowanie
---



API udostępnione przez SDK do Visual Studio pozwala na olbrzymie zmiany w IDE. Niestety nie zawsze to co chcemy zrobić jest możliwe w oficjalny sposób. W tym wpisie przedstawię sposób na modyfikowanie elementów interfejsu Visual Studio, które nie są możliwe poprzez API.  *Będziemy hakowali Visuala*  :)




## API do Visual Studio - mnogość możliwość, ale jednak z ograniczeniami


Ilość elementów, [jakie można rozszerzać](https://www.dobreprogramy.pl/djfoxer/Jakie-elementy-Visual-Studio-moga-byc-rozszerzane-przez-deweloperow,80061.html) może spowodować zagubienie na samym początku. Programiści mogą przy pomocy SDK modyfikować niemalże wszystko od dodania menu, poprzez własny edytor, na customowym, dostosowanym do konkretnych potrzeb nowym IDE kończąc.

Jednakże udostępnione API nie pozwala na duże ingerencje w każdym aspekcie. Chociażby pasek statusu na dole ma niemalże zerowe możliwości rozbudowy. Nie jest to jednak przeszkodą dla programistów .NET...



## Visual Studio też jest aplikacją WPF


Podejdźmy jednak do IDE od Microsoftu z innej strony. Powłoka Visual Studio w wersji 2010 została całkowicie przepisana na WPF. Użyto również MEF ([opis we wcześniejszym wpisie](https://www.dobreprogramy.pl/djfoxer/Managed-Extensibility-Framework-system-pluginow-do-aplikacji-.NET-od-Microsoftu,80021.html)) jako frameworku do pisania rozszerzeń i bazy pod nową odsłonę edytora.

Taka wiedza pozwoli nam na zaprzęgniecie do pracy narzędzi, które analizują strukturę drzewa UI aplikacji napisanych w WPF. W prosty sposób przejrzymy budowę programu i rozszerzymy go o nowe elementy. Bez oficjalnego API dobierzemy się do każdego elementu i rozbudujemy IDE o własne kontrolki. Jednym z takich narzędzi jest... 



## Snoop, the WPF Spy Utility





![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-27-_15_/g_-_608x405_-_-_80126x20170326233728_0.png



[Snoop](https://snoopwpf.codeplex.com/) jest świetnym narzędziem do wizualizacji warstw elementów graficznych w aplikacji WPF. Potrafi ono analizować dynamicznie strukturę kontrolek w uruchomionej aplikacji. Wystarczy kursorem wskazać program i można już przechodzić po drzewie elementów.



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-27-_15_/g_-_608x405_-_-_80126x20170327174420_0.PNG



Snoop posiada także ciekawy wizualizator warstw w analizowanej aplikacji. 



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-27-_15_/g_-_608x405_-_-_80126x20170327174420_1.PNG



Program na żywo pokazuje całą strukturę widoku, pozwala to na szybki podgląd ułożenia poszczególnych elementów z właściwościami, DataContextem, eventami i metodami. Co ważne umożliwia on zmianę tych danych  *w locie* .



## Dobieramy się do niedostępnych elementów Visual Studio


Jak zatem rozszerzyć IDE o własne kontrolki? Wystarczy z poziomu Snoopa znaleźć interesujący nas element i zapamiętać jego nazwę oraz typ. Dla przykładu rozszerzymy o własną kontrolkę dolny pasek w Visual Studio, StatusBar:



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-27-_15_/g_-_608x405_-_-_80126x20170327181039_0.PNG



Następnie w C# wyszukamy go dynamicznie przy pomocy  *VisualTreeHelper&#39;a* . Użyjemy do tego kodu ze [StackOverflow](http://stackoverflow.com/a/1759923): 


```csharp

public static T FindChild&lt;T&gt;(DependencyObject parent, string childName)
   where T : DependencyObject
{    
  // Confirm parent and childName are valid. 
  if (parent == null) return null;

  T foundChild = null;

  int childrenCount = VisualTreeHelper.GetChildrenCount(parent);
  for (int i = 0; i &lt; childrenCount; i++)
  {
    var child = VisualTreeHelper.GetChild(parent, i);
    // If the child is not of the request child type child
    T childType = child as T;
    if (childType == null)
    {
      // recursively drill down the tree
      foundChild = FindChild&lt;T&gt;(child, childName);

      // If the child is found, break so we do not overwrite the found child. 
      if (foundChild != null) break;
    }
    else if (!string.IsNullOrEmpty(childName))
    {
      var frameworkElement = child as FrameworkElement;
      // If the child&#39;s name is set for search
      if (frameworkElement != null &amp;&amp; frameworkElement.Name == childName)
      {
        // if the child&#39;s name is of the request name
        foundChild = (T)child;
        break;
      }
    }
    else
    {
      // child element found.
      foundChild = (T)child;
      break;
    }
  }

  return foundChild;
}

```


W naszym kodzie wtyczki pobranie StatusBara z Visual Studio wyglądać będzie tak:


```csharp

var statusBarObj = UIHelper.FindChildControl&lt;DockPanel&gt;(
Application.Current.MainWindow,&quot;StatusBarPanel&quot;);

```


Dodajmy teraz jeszcze jakiś dowolny przycisk, aby pokazać, że faktycznie dobraliśmy się bezpośrednio do paska statusu:


```csharp

var button = new Button();
button.Content = &quot;Klikamy!&quot;;
statusBarObj.Children.Insert(0, button);

```


Oto efekt końcowy, niemożliwe stało się możliwe:



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-27-_15_/g_-_608x405_-_-_80126x20170327181039_1.PNG



W kolejnym wpisie wykorzystamy zdobytą wiedzę do wyświetlenia timera na pasku statusu!
