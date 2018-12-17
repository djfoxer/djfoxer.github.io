---
layout:     post
title:      Własny dodatek Timer Pomodoro na pasku statusu Visual Studio
date:       2017-03-31 17:10:00
summary:    W poprzednim wpisie  pokazywałem jak rozszerzyć Visual Studio o elementy, do których dostęp nie jest możliwy poprzez SDK. Przyszedł czas zatem na wykorzystanie wiedzy w praktyce. Napiszemy podstawy wtyczki HealthyWithVS, w których będzie możliwe pokazanie na pasku zadań timera z pomidorkiem, zgodnie z techniką Pomodoro. <!----><!----><!----><!---->Zaczniemy oczywiście od stworzenia projektu typu V...
categories: windows oprogramowanie programowanie
slug: Wlasny-dodatek-Timer-Pomodoro-na-pasku-statusu-Visual-Studio,80247.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331004545_1.png
---



W [poprzednim wpisie](http://blog.djfoxer.pl/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html)  pokazywałem jak rozszerzyć Visual Studio o elementy, do których dostęp nie jest możliwy poprzez SDK. Przyszedł czas zatem na wykorzystanie wiedzy w praktyce. Napiszemy podstawy wtyczki HealthyWithVS, w których będzie możliwe pokazanie na pasku zadań timera z pomidorkiem, [zgodnie z techniką Pomodoro](http://blog.djfoxer.pl/Technika-Pomodoro-efektywne-zarzadzanie-czasem-pracy,79724.html). 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331004545_1.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331003927_0.png)






Zaczniemy oczywiście od stworzenia projektu typu  *VSIX Project* , który jest bazą dla wtyczek do Visual Studio. Pierwszym elementem jaki dodamy będzie górne menu, z którego aktywujemy pasek z naszym timerem z pomidorkiem.

Do projektu zatem dorzucamy nowy Item typu  *Custom Command*  (dostępny w  *Extenibility* ). Tak to wygląda (TomatoStatusBar.xaml jest kontrolką WPF z timerem, o czym później): 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331003927_1.png)



Wygenerowany kod będzie jedynie udostępniał podmenu do menu Tools. Zróbmy jednak...



## Własne menu w Visual Studio



Dodanie menu wymaga edycji pliku  *vsct* , który odpowiada za rozmieszenie edytowalnego elementu UI na oknie VS. Jeśli dodaliśmy plik typu  *Custom Command*  z okienka  IDE, wówczas taki plik zostanie stworzony automatycznie z wygenerowanym podstawom przyciskiem. 

Czym jest  *vsct* ? Jest to dokument  *xml* , w którym rozmieszczamy przyciski, menu czy grupy obiektów. Każdy z elementów ma guid, określający jego przynależność do grupy, a także id służący do identyfikacji w grupie. Plik definiuje położenie elementów w oknie IDE i między sobą. Określamy zatem własne elementy (jak przyciski czy menu) i podpinany je pod istniejące już elementy (za pomocą znacznika  *Parent* ). Na początku wydaje się to trochę skompilowane, ale po chwili można już opanować podstawy, potrzebne do stworzenia prostych elementów graficznych. Zatem do dzieła!

Do gotowego kodu dorzucamy informację o własnym, menu podpiętym pod główny pasek VS:



```html

<Menus>
  <Menu guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
    <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
    <Strings>
      <ButtonText>Healthy With VS</ButtonText>
    </Strings>
  </Menu>
</Menus>

```



 *IDG_VS_MM_TOOLSADDINS*  wskazuje na pasek menu górnego w IDE, do którego podepniemy nasze menu. Tutaj również zauważymy, iż wskazywany rodzic ma guid równy stałej  *guidSHLMainMenu* , co określa złączenie stworzonego elementu bezpośrednio z wybranym miejscem w Visual Studio.

Tworzymy również grupę, która będzie podpięta pod nasze górne menu:



```html

<Groups>
  <Group guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="MyMenuGroup" priority="0x0600">
    <Parent guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="TopLevelMenu"/>
  </Group>
</Groups>


```



Na koniec w sekcji  *Buttons*  dodajemy przycisk, który podpinamy do grupy:



```html

<Buttons>
  <Button guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="CommandShowTomatoStatusBarId" priority="0x0100" type="Button">
    <Parent guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="MyMenuGroup" />
    <Icon guid="guidImageStatus" id="bmpPic1" />
    <Strings>
      <CommandName>cmdidMyFirstCommand</CommandName>
      <ButtonText>Show Pomodoro Status Bar</ButtonText>
    </Strings>
  </Button>
</Buttons>

```



Nie zapomnijmy jeszcze o załadowaniu grafik i nadaniu wartości poszczególnym id w naszej strukturze. Dokonamy tego poprzez znaczniki  *GuidSymbol*  i  *IDSymbol* , zaś grafiki ładujemy w  *Bitmaps* .

W celu nie przeciągania tej części (i nie zaciemniania rozwiązania) udostępnię finalną wersję pliku. Omawiany xml prezentuje się następująco:



```html

<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <Extern href="stdidcmd.h"/>
  <Extern href="vsshlids.h"/>
  <Commands package="guidCommandShowTomatoStatusBarPackage">
    <Groups>
      <Group guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="MyMenuGroup" priority="0x0600">
        <Parent guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="TopLevelMenu"/>
      </Group>
    </Groups>
    <Menus>
      <Menu guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
        <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
        <Strings>
          <ButtonText>Healthy With VS</ButtonText>
        </Strings>
      </Menu>
    </Menus>
    <Buttons>
      <Button guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="CommandShowTomatoStatusBarId" priority="0x0100" type="Button">
        <Parent guid="guidCommandShowTomatoStatusBarPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImageStatus" id="bmpPic1" />
        <Strings>
          <CommandName>cmdidMyFirstCommand</CommandName>
          <ButtonText>Show Pomodoro Status Bar</ButtonText>
        </Strings>
      </Button>
    </Buttons>
    <Bitmaps>
      <Bitmap guid="guidImageStatus" href="..\Resources\statusbar.png" usedList="bmpPic1"/>
    </Bitmaps>
  </Commands>
  <Symbols>
    <GuidSymbol name="guidCommandShowTomatoStatusBarPackage" value="{03b63e3b-39cd-4c93-98b6-42cf447f55e6}" />
    <GuidSymbol name="guidCommandShowTomatoStatusBarPackageMenu" value="{fffe3072-816e-43db-81c7-28e48c5b788b}" >
    </GuidSymbol>
    <GuidSymbol name="guidCommandShowTomatoStatusBarPackageCmdSet" value="{2089436a-ed0c-4bae-b1a3-d16000d5e669}">
      <IDSymbol name="MyMenuGroup" value="0x1020" />
      <IDSymbol name="CommandShowTomatoStatusBarId" value="0x0100" />
      <IDSymbol name="TopLevelMenu" value="0x1021"/>
    </GuidSymbol>
    <GuidSymbol name="guidImageStatus" value="{47a9ad46-e6a2-4d57-885c-9cefda0253d9}" >
      <IDSymbol name="bmpPic1" value="1" />
    </GuidSymbol>
  </Symbols>
</CommandTable>


```



Efektem pracy jest gotowe menu:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331003926_0.png)

 



## Timer Pomodoro na pasku statusu


Teraz dodajmy timer na pasku statusu. Zaczniemy prosto, od stworzenia kontrolki w XAMLu (u mnie TomatoStatusBar.xaml). Wykorzystamy do tego kod, który był już przedstawiony [we wpisie z tworzeniem Toolboxa z timerem](http://blog.djfoxer.pl/Pierwszy-dodatek-do-Visual-Studio-timer-w-okienku-IDE,79926.html). 

Od strony C# będzie to niemalże identyczny kod, zaś widok będzie jedynie trochę doszlifowany, aby zmieścił się w małe miejsce na dole okna Visual Studio. Widok zawiera ikonkę pomidora, timer odliczający od 25 minut w dół i przycisk play/pauza oraz stop. Dodatkowo gdy zegar dojdzie do końca (00:00) z głośników wydobędzie się sygnał budzika :)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331003926_1.png)



Wspomagając się kodem, omawianym [we wpisie o Hakowaniu  *Visual Studio* ](http://blog.djfoxer.pl/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html)  dodamy stworzoną kontrolkę do dolnego paska. Zaczniemy od podczepienia się do eventu menu, które stworzyliśmy w poprzednim punkcie. Jeśli pliki powstał z kreatora z szablonu, wówczas wchodzimy w klasę będącą implementacją akcji w naszym pakiecie (w moim przypadku jest to  *CommandShowTomatoStatusBar.cs* )

Na początku dobieramy się do ukrytego StatusBara w VS wg sposobu [z wcześniejszego wpisu](http://blog.djfoxer.pl/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html) :



```csharp

var statusBarObj = UIHelper.FindChildControl<DockPanel>(
Application.Current.MainWindow, "StatusBarPanel");

```



a następnie wstrzykujemy naszą kontrolkę WPF na początek paska:



```csharp

statusBarObj.Children.Insert(0, new TomatoStatusBar());

```



W ten sposób otrzymujemy w pełni działający timer na bazie techniki Pomodoro:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331003920_0.png)




W kolejnych wpisach będziemy rozszerzali możliwości wtyczki o ćwiczenia w formie graficznych obrazków.




> Źródła dostępne są na GitHubie (branch master i POC):
> [https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-31-_28_/g_-_-x-_-_-_x20170331004248_0.png)


 