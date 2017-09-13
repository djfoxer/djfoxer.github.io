---
layout:     post
title:      Własny dodatek Timer Pomodoro na pasku statusu Visual Studio
date:       2017-03-31 17:10:00
summary:    W poprzednim wpisie pokazywałem jak rozszerzyć Visual Studio o elementy, do których dostęp nie jest możliwy poprzez SDK. Przyszedł czas zatem na wykorzystanie wiedzy w praktyce. Napiszemy podstawy wtyczki HealthyWithVS, w których będzie możliwe pokazanie na pasku zadań timera z pomidorkiem, zgodnie ...
categories: windows oprogramowanie programowanie
---



W [poprzednim wpisie](https://www.dobreprogramy.pl/djfoxer/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html) pokazywałem jak rozszerzyć Visual Studio o elementy, do których dostęp nie jest możliwy poprzez SDK. Przyszedł czas zatem na wykorzystanie wiedzy w praktyce. Napiszemy podstawy wtyczki HealthyWithVS, w których będzie możliwe pokazanie na pasku zadań timera z pomidorkiem, [zgodnie z techniką Pomodoro](https://www.dobreprogramy.pl/djfoxer/Technika-Pomodoro-efektywne-zarzadzanie-czasem-pracy,79724.html).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331004545_1.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331003927_0.png)






Zaczniemy oczywiście od stworzenia projektu typu  *VSIX Project* , który jest bazą dla wtyczek do Visual Studio. Pierwszym elementem jaki dodamy będzie górne menu, z którego aktywujemy pasek z naszym timerem z pomidorkiem.

Do projektu zatem dorzucamy nowy Item typu  *Custom Command*  (dostępny w  *Extenibility* ). Tak to wygląda (TomatoStatusBar.xaml jest kontrolką WPF z timerem, o czym później): 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331003927_1.png)



Wygenerowany kod będzie jedynie udostępniał podmenu do menu Tools. Zróbmy jednak...



## Własne menu w Visual Studio



Dodanie menu wymaga edycji pliku  *vsct* , który odpowiada za rozmieszenie edytowalnego elementu UI na oknie VS. Jeśli dodaliśmy plik typu  *Custom Command*  z okienka  IDE, wówczas taki plik zostanie stworzony automatycznie z wygenerowanym podstawom przyciskiem. 

Czym jest  *vsct* ? Jest to dokument  *xml* , w którym rozmieszczamy przyciski, menu czy grupy obiektów. Każdy z elementów ma guid, określający jego przynależność do grupy, a także id służący do identyfikacji w grupie. Plik definiuje położenie elementów w oknie IDE i między sobą. Określamy zatem własne elementy (jak przyciski czy menu) i podpinany je pod istniejące już elementy (za pomocą znacznika  *Parent* ). Na początku wydaje się to trochę skompilowane, ale po chwili można już opanować podstawy, potrzebne do stworzenia prostych elementów graficznych. Zatem do dzieła!

Do gotowego kodu dorzucamy informację o własnym, menu podpiętym pod główny pasek VS:


```html

&lt;Menus&gt;
  &lt;Menu guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;TopLevelMenu&quot; priority=&quot;0x700&quot; type=&quot;Menu&quot;&gt;
    &lt;Parent guid=&quot;guidSHLMainMenu&quot; id=&quot;IDG_VS_MM_TOOLSADDINS&quot; /&gt;
    &lt;Strings&gt;
      &lt;ButtonText&gt;Healthy With VS&lt;/ButtonText&gt;
    &lt;/Strings&gt;
  &lt;/Menu&gt;
&lt;/Menus&gt;

```


 *IDG_VS_MM_TOOLSADDINS*  wskazuje na pasek menu górnego w IDE, do którego podepniemy nasze menu. Tutaj również zauważymy, iż wskazywany rodzic ma guid równy stałej  *guidSHLMainMenu* , co określa złączenie stworzonego elementu bezpośrednio z wybranym miejscem w Visual Studio.

Tworzymy również grupę, która będzie podpięta pod nasze górne menu:


```html

&lt;Groups&gt;
  &lt;Group guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;MyMenuGroup&quot; priority=&quot;0x0600&quot;&gt;
    &lt;Parent guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;TopLevelMenu&quot;/&gt;
  &lt;/Group&gt;
&lt;/Groups&gt;


```


Na koniec w sekcji  *Buttons*  dodajemy przycisk, który podpinamy do grupy:


```html

&lt;Buttons&gt;
  &lt;Button guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;CommandShowTomatoStatusBarId&quot; priority=&quot;0x0100&quot; type=&quot;Button&quot;&gt;
    &lt;Parent guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;MyMenuGroup&quot; /&gt;
    &lt;Icon guid=&quot;guidImageStatus&quot; id=&quot;bmpPic1&quot; /&gt;
    &lt;Strings&gt;
      &lt;CommandName&gt;cmdidMyFirstCommand&lt;/CommandName&gt;
      &lt;ButtonText&gt;Show Pomodoro Status Bar&lt;/ButtonText&gt;
    &lt;/Strings&gt;
  &lt;/Button&gt;
&lt;/Buttons&gt;

```


Nie zapomnijmy jeszcze o załadowaniu grafik i nadaniu wartości poszczególnym id w naszej strukturze. Dokonamy tego poprzez znaczniki  *GuidSymbol*  i  *IDSymbol* , zaś grafiki ładujemy w  *Bitmaps* .

W celu nie przeciągania tej części (i nie zaciemniania rozwiązania) udostępnię finalną wersję pliku. Omawiany xml prezentuje się następująco:


```html

&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;CommandTable xmlns=&quot;http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable&quot; xmlns:xs=&quot;http://www.w3.org/2001/XMLSchema&quot;&gt;
  &lt;Extern href=&quot;stdidcmd.h&quot;/&gt;
  &lt;Extern href=&quot;vsshlids.h&quot;/&gt;
  &lt;Commands package=&quot;guidCommandShowTomatoStatusBarPackage&quot;&gt;
    &lt;Groups&gt;
      &lt;Group guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;MyMenuGroup&quot; priority=&quot;0x0600&quot;&gt;
        &lt;Parent guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;TopLevelMenu&quot;/&gt;
      &lt;/Group&gt;
    &lt;/Groups&gt;
    &lt;Menus&gt;
      &lt;Menu guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;TopLevelMenu&quot; priority=&quot;0x700&quot; type=&quot;Menu&quot;&gt;
        &lt;Parent guid=&quot;guidSHLMainMenu&quot; id=&quot;IDG_VS_MM_TOOLSADDINS&quot; /&gt;
        &lt;Strings&gt;
          &lt;ButtonText&gt;Healthy With VS&lt;/ButtonText&gt;
        &lt;/Strings&gt;
      &lt;/Menu&gt;
    &lt;/Menus&gt;
    &lt;Buttons&gt;
      &lt;Button guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;CommandShowTomatoStatusBarId&quot; priority=&quot;0x0100&quot; type=&quot;Button&quot;&gt;
        &lt;Parent guid=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; id=&quot;MyMenuGroup&quot; /&gt;
        &lt;Icon guid=&quot;guidImageStatus&quot; id=&quot;bmpPic1&quot; /&gt;
        &lt;Strings&gt;
          &lt;CommandName&gt;cmdidMyFirstCommand&lt;/CommandName&gt;
          &lt;ButtonText&gt;Show Pomodoro Status Bar&lt;/ButtonText&gt;
        &lt;/Strings&gt;
      &lt;/Button&gt;
    &lt;/Buttons&gt;
    &lt;Bitmaps&gt;
      &lt;Bitmap guid=&quot;guidImageStatus&quot; href=&quot;..\Resources\statusbar.png&quot; usedList=&quot;bmpPic1&quot;/&gt;
    &lt;/Bitmaps&gt;
  &lt;/Commands&gt;
  &lt;Symbols&gt;
    &lt;GuidSymbol name=&quot;guidCommandShowTomatoStatusBarPackage&quot; value=&quot;{03b63e3b-39cd-4c93-98b6-42cf447f55e6}&quot; /&gt;
    &lt;GuidSymbol name=&quot;guidCommandShowTomatoStatusBarPackageMenu&quot; value=&quot;{fffe3072-816e-43db-81c7-28e48c5b788b}&quot; &gt;
    &lt;/GuidSymbol&gt;
    &lt;GuidSymbol name=&quot;guidCommandShowTomatoStatusBarPackageCmdSet&quot; value=&quot;{2089436a-ed0c-4bae-b1a3-d16000d5e669}&quot;&gt;
      &lt;IDSymbol name=&quot;MyMenuGroup&quot; value=&quot;0x1020&quot; /&gt;
      &lt;IDSymbol name=&quot;CommandShowTomatoStatusBarId&quot; value=&quot;0x0100&quot; /&gt;
      &lt;IDSymbol name=&quot;TopLevelMenu&quot; value=&quot;0x1021&quot;/&gt;
    &lt;/GuidSymbol&gt;
    &lt;GuidSymbol name=&quot;guidImageStatus&quot; value=&quot;{47a9ad46-e6a2-4d57-885c-9cefda0253d9}&quot; &gt;
      &lt;IDSymbol name=&quot;bmpPic1&quot; value=&quot;1&quot; /&gt;
    &lt;/GuidSymbol&gt;
  &lt;/Symbols&gt;
&lt;/CommandTable&gt;


```


Efektem pracy jest gotowe menu:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331003926_0.png)

 



## Timer Pomodoro na pasku statusu


Teraz dodajmy timer na pasku statusu. Zaczniemy prosto, od stworzenia kontrolki w XAMLu (u mnie TomatoStatusBar.xaml). Wykorzystamy do tego kod, który był już przedstawiony [we wpisie z tworzeniem Toolboxa z timerem](https://www.dobreprogramy.pl/djfoxer/Pierwszy-dodatek-do-Visual-Studio-timer-w-okienku-IDE,79926.html).

Od strony C# będzie to niemalże identyczny kod, zaś widok będzie jedynie trochę doszlifowany, aby zmieścił się w małe miejsce na dole okna Visual Studio. Widok zawiera ikonkę pomidora, timer odliczający od 25 minut w dół i przycisk play/pauza oraz stop. Dodatkowo gdy zegar dojdzie do końca (00:00) z głośników wydobędzie się sygnał budzika :)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331003926_1.png)



Wspomagając się kodem, omawianym [we wpisie o Hakowaniu  *Visual Studio* ](https://www.dobreprogramy.pl/djfoxer/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html) dodamy stworzoną kontrolkę do dolnego paska. Zaczniemy od podczepienia się do eventu menu, które stworzyliśmy w poprzednim punkcie. Jeśli pliki powstał z kreatora z szablonu, wówczas wchodzimy w klasę będącą implementacją akcji w naszym pakiecie (w moim przypadku jest to  *CommandShowTomatoStatusBar.cs* )

Na początku dobieramy się do ukrytego StatusBara w VS wg sposobu [z wcześniejszego wpisu](https://www.dobreprogramy.pl/djfoxer/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html):


```csharp

var statusBarObj = UIHelper.FindChildControl&lt;DockPanel&gt;(
Application.Current.MainWindow, &quot;StatusBarPanel&quot;);

```


a następnie wstrzykujemy naszą kontrolkę WPF na początek paska:


```csharp

statusBarObj.Children.Insert(0, new TomatoStatusBar());

```


W ten sposób otrzymujemy w pełni działający timer na bazie techniki Pomodoro:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331003920_0.png)




W kolejnych wpisach będziemy rozszerzali możliwości wtyczki o ćwiczenia w formie graficznych obrazków.


<blockquote>
<p>Źródła dostępne są na GitHubie (branch master i POC):

[https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_14_/g_-_608x405_-_-_80247x20170331004248_0.png)


 