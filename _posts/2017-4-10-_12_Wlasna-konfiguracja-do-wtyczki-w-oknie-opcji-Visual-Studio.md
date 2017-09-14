---
layout:     post
title:      Własna konfiguracja do wtyczki w oknie opcji Visual Studio
date:       2017-04-10 18:52:00
summary:    Jakiś czas temu przedstawiłem sposób na umieszczenie Timera Pomodoro na pasku statusu w Visual Studio. W kolejnym kroku dodamy opcje konfiguracyjne do wtyczki w standardowym oknie opcji IDE.Do tej pory, aby pokazać timera na pasu statusu trzeba było ręcznie wywołać z menu opcję dodająca element do Visual Studio. Spróbujmy zatem skonfigurować tą poprzez oko opcji w IDE.Autostart wtyczek w Visual St...
categories: windows oprogramowanie programowanie
slug: Wlasna-konfiguracja-do-wtyczki-w-oknie-opcji-Visual-Studio,80415.html
---



Jakiś czas temu przedstawiłem sposób na [umieszczenie Timera Pomodoro na pasku statusu w Visual Studio](http://blog.djfoxer.pl/Wlasny-dodatek-Timer-Pomodoro-na-pasku-statusu-Visual-Studio,80247.html). W kolejnym kroku dodamy opcje konfiguracyjne do wtyczki w standardowym oknie opcji IDE.


Do tej pory, aby pokazać timera na pasu statusu trzeba było ręcznie wywołać z menu opcję dodająca element do Visual Studio. Spróbujmy zatem skonfigurować tą poprzez oko opcji w IDE.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-10-_12_/g_-_608x405_-_-_80415x20170410185129_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-10-_12_/g_-_608x405_-_-_80415x20170410184228_0.PNG)



## Autostart wtyczek w Visual Studio

Nasza wtyczka składa się z paczek ( *Packaga* ). W celu automatycznego uruchomienia dodatku przy starcie IDE musimy dodać atrybut do naszej klasy dziedziczącej po  *Package* .


```csharp

[ProvideAutoLoad(VSConstants.UICONTEXT.ShellInitialized_string)]
public sealed class CommandShowTomatoStatusBarPackage : Package

```


Atrybut  *ProvideAutoLoad*  oznacza uruchomienie paczkę przy starce, zaś parametr określa kiedy ma to zrobić. Mamy kilka opcji:



  * ShellInitialized_string


  * NoSolution_string


  * EmptySolution_string


  * SolutionBuilding_string


  * ...



W moim przypadku będzie to  *ShellInitialized_string* , czyli załadownie solucji, kiedy UI VS zostanie w pełni załadowane.

 

## Okienko opcji w Visual Studio

Własne okienko w oknie konfiguracyjnym można umieścić bardzo prosto. Dodajemy do solucji nowy element  *Visual Studio Package* . Następnie tworzymy nową klasę, która dziedziczyć będzie po  *DialogPage* :


```csharp

public class OptionPage : DialogPage

```


W kolejnym kroku dodamy zmienną typu bool, która zostanie przez IDE potraktowana jako opcja w menu i wyrenderowana w postaci grida z wyborem wartości True/False. W tym przypadku będzie ona określać, czy Timer Pomodoro ma załadować się przy starcie Visual Studio lub nie:


```csharp


[Category(Consts.OptionsCategoryBasicName)]
[DisplayName(Consts.OptionsCategoryBasicStatusBarAutostartText)]
[Description(Consts.OptionsCategoryBasicStatusBarAutostartInfoText)]
public bool AutostartPomodoroStatusBar {get; set;}
```


 *Category*  określa nazwę podwęzła w naszych opcjach, zaś  *DisplayName*  i  *Description*  są odpowiednio nazwami dla zmiennej i jej opisu w okienku opcji.

Teraz łączymy stworzony przed chwilą Visual Studio Package z okienkiem konfiguracji. Robimy to za pomocą dodania atrybutu do klasy dziedziczącej z  *Package* :


```csharp

[ProvideOptionPage(typeof(OptionPage),
Consts.PluginName, Consts.OptionsCategoryBasicName, 0, 0, true)]

```


Stworzona klasa  *OptionPage*  (dziedzicząca po  *DialogPage* ) będzie podczepiona pod drzewko opcji w konfiguracji IDE ( *Consts.PluginName*  to korzeń, a jest nazwą liścia  *Consts.OptionsCategoryBasicName* ). Efekt mamy następujący:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-10-_12_/g_-_608x405_-_-_80415x20170410184228_0.PNG)



## Odczyt danych z okienka opcji

Jak odczytywać aktualne dane z okienka konfiguracji IDE? Robimy to w następujący sposób:


```csharp
((OptionPage)GetDialogPage(typeof(OptionPage))).AutostartPomodoroStatusBar;

```


 *GetDialogPage*  jest metodą w klasie dziedziczącej po  *Package* . W ten sposób z okienka, które powstała poprzez stworzenie klasy  *OptionPage* , odczytujemy zmienną  *AutostartPomodoroStatusBar* .


W tak dość nieskomplikowany sposób otrzymaliśmy proste okienko konfiguracyjne w IDE.


> Źródła dostępne są na GitHubie (branch master i POC):
> [https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-10-_12_/g_-_608x405_-_-_80415x20170410184234_0.png)

