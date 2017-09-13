---
layout:     post
title:      Managed Extensibility Framework — system pluginów do aplikacji .NET od Microsoftu 
date:       2017-03-22 16:42:00
summary:    W poprzednim wpisie pokazałem jak szybko stworzyć własne okienko w Visual Studio (timer w okienku IDE). Dziś opiszę MEF, czyli framework do tworzenia lekkich aplikacji i pisania rozszerzeń do nich. To właśnie na nim opiera się IDE od Microsoftu.MEF w teoriiObecnie MEF (Managed Extensibility Framewor...
categories: windows porady programowanie
---



W poprzednim wpisie pokazałem jak szybko stworzyć własne okienko w Visual Studio ([timer w okienku IDE](https://www.dobreprogramy.pl/djfoxer/Pierwszy-dodatek-do-Visual-Studio-timer-w-okienku-IDE,79926.html)). Dziś opiszę MEF, czyli framework do tworzenia lekkich aplikacji i pisania rozszerzeń do nich. To właśnie na nim opiera się IDE od Microsoftu.



## MEF w teorii


Obecnie MEF (Managed Extensibility Framework) jest komponentem .NET 4.0. Biblioteka powstała jako odpowiedź na zapotrzebowania programistów w tworzeniu aplikacji, które mogłyby być rozszerzalne poprzez zewnętrzne pluginy (reużywalne). Jest on zbiorem wcześniejszych doświadczeń, który pozwala w prosty sposób na zaimplementowanie systemu rozszerzeń w każdej aplikacji .NET, bez tworzenia kolejnego frameworku od zera.



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-22-_17_/g_-_608x405_-_-_80021x20170321131143_0.png



MEF można uznać za bibliotekę pozwalająca na Dependency Injection opartą na atrybutach. Pozwala ona na tworzenie aplikacji na zasadzie odkrywania (wyszukiwania) rozszerzeń i ładowania ich dynamicznie do programu. Takie dodatki mogą być reużywalne przez różne aplikacje. MEF umożliwia dla programu, do którego ładowane są wtyczki, stworzenie sposobu na identyfikację i walidację takiego zewnętrznego kodu,  a także jego uruchomienie.

Managed Extensibility Framework pozwala zarówno na tworzenie wtyczek, jak i aplikacji, które będę z nich korzystać. Framework umożliwia także rozszerzanie platformy o własne rozwiązania i biblioteki, bazując na MEF. Visual Studio korzysta z MEF i pozwala w ten sposób na pisanie dodatków, powiększających możliwości IDE. 



### Composition container, catalog, parts



Aplikacje pisane w MEF bazują na podstawowych elementach: kontener z kompoyzcją (composition container), katalog (catalog) i elementy (parts).




  * parts - podstawowa jednostka MEF, która umożliwia import i eksport funkcjonalności poprzez kontrakt; kontrakt (contract) jest sposobem na łączenie poszczególnych części 


  * composition container - jest to rdzeń rozwiązań MEF, to tutaj przechowane są dostępne elementy (parts), zarządza się instancjami poszczególnych elementów i w tym miejscu następuje kompozycja (łączenie wymaganych części [imports] z tymi dostępnymi [exports]) 


  * catalog - jest to abstrakcyjne miejsce, które gromadzi elementy do użycia w kontenerze z kompozycją; MEF udostępnia katalogi, które pozwalają na odkrywanie (discover) elementów (parts) poprzez typy (TypeCatalog), assembly (AssemblyCatalog),  foldery (DirecotryCatalog) i inne katalogi (AggregateCatalog) 


 



## MEF w praktyce


Zobaczmy zatem jak sprawuje się MEF. W tym celu tworzymy zwykłą aplikację konsolową, którą wykorzysta mechanizm pluginów (pamiętając jednocześnie o dodaniu referencji  *System.ComponentModel.Composition* !).



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-22-_17_/g_-_608x405_-_-_80021x20170321140941_0.PNG



Aplikacja konsolowa będzie uruchamiała naszego  *hosta* , który to będzie rozszerzony o autorski plugin.


```csharp

using System;

namespace MEFExample
{
    class Program
    {
        static void Main(string
```
 args)
        {
            HostApp hostApp = new HostApp();
            hostApp.Start();
            //just wait to see results
            Console.ReadKey();
        }
    }
}
[/code]

Stwórzmy zatem prosty interface do pluginu, a także jego implementację.


```csharp

namespace MEFExample
{
    public interface IMessagePlugin
    {
        string GetMessage();
    }
}


```



```csharp

using System.ComponentModel.Composition;

namespace MEFExample
{
    
```

    public class MessagePlugin : IMessagePlugin
    {
        public string GetMessage()
        {
            return &quot;Message from plugin&quot;;
        }
    }
}

[/code]

W ty miejscu nasza implementacja pluginu jest oznaczona atrybutem  *Export* . Oznacza to tyle, że eksportujemy nasz kod (implementację) do kontenera.

Teraz przyszedł czas na implementację naszego programu hostującego, który będzie rozszerzany przez plugin.


```csharp

using System;
using System.ComponentModel.Composition;
using System.ComponentModel.Composition.Hosting;

namespace MEFExample
{
    public class HostApp
    {
        
```

        public IMessagePlugin MessageToClient { get; set; }

        public void Start()
        {
            Compose();
            Console.WriteLine(MessageToClient.GetMessage());
        }

        private void Compose()
        {
            AssemblyCatalog catalog = 
             new AssemblyCatalog(System.Reflection.Assembly.GetExecutingAssembly());
            CompositionContainer container = new CompositionContainer(catalog);
            container.ComposeParts(this);
        }
    }
}
[/code]

Zauważmy dwa ważne elementy: atrybut  *Import*  i metodę  *Compose* . Dodanie atrybutu  *Import*  zaimportuje z kontenera implementację IMessagePlugin, która została dodana wcześniej przy eksporcie. 

Metoda Compose jest najważniejsza tutaj. W tym miejscu powiadamiamy MEF, iż abstrakcyjny katalog powinien wyszukać elementów (parts) z biblioteki, a tą biblioteką jest aktualnie wykonywane assembly:

 
```csharp

AssemblyCatalog catalog = 
             new AssemblyCatalog(System.Reflection.Assembly.GetExecutingAssembly());


```


W kolejnym kroku dodajemy powyższy katalog do kontenera z kompozycją:

 
```csharp

CompositionContainer container = new CompositionContainer(catalog);

```


Na koniec łączymy całość i przekazujemy jako parametr instancję, która ma zaimportować elementy z kontenera. W naszym przypadku jest to  *this* , czyli aktualna instancja  *HostApp* , zawierająca proporcję  *MessageToClient*  z atrybutem  *Import* . 

 
```csharp

container.ComposeParts(this);

```


Po uruchomieniu otrzymamy taki ekran:



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-22-_17_/g_-_608x405_-_-_80021x20170321220233_0.PNG





## MEF i Visual Studio


Po co nam wiedza o MEF? Otóż edytor w Visual Studio został oparty na MEF. Zatem napisanie jakiegokolwiek pluginu do IDE od Microsoftu będzie wymagało dotknięcia do MEF. O czym już konkretniej w kolejnej części.



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-22-_17_/g_-_608x405_-_-_80021x20170321220231_0.png




<blockquote>
<p>Źródła dostępne są na GitHubie (branch master i POC):

[https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-3-22-_17_/g_-_608x405_-_-_80021x20170321220545_0.png

