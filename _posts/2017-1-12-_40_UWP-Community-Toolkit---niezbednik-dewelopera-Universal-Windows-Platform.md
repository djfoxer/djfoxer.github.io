---
layout:     post
title:      UWP Community Toolkit — niezbędnik dewelopera Universal Windows Platform
date:       2017-01-12 17:26:00
summary:    Tworzenie aplikacji na najświeższą platformę Windows (Universal Windows Platform) nie powinno sprawiać dużych problemów nawet początkującym osobom w tym temacie. Warto jednak już od pierwszych kroków wyposażyć się w ciekawy zbiór bibliotek od Microsoftu, który uprzyjemni pracę w UWP. Zróżnicowany zestaw pomocnych elementów znacznie usprawni programowanie na platformie Windows.<!----><!---->UWP Com...
categories: windows porady programowanie
slug: UWP-Community-Toolkit-niezbednik-dewelopera-Universal-Windows-Platform,78412.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_40_/g_-_-x-_-_-_x20170112003503_0.jpg
---



Tworzenie aplikacji na najświeższą platformę Windows (Universal Windows Platform) nie powinno sprawiać dużych problemów nawet początkującym osobom w tym temacie. Warto jednak już od pierwszych kroków wyposażyć się w ciekawy zbiór bibliotek od Microsoftu, który uprzyjemni pracę w UWP. Zróżnicowany zestaw pomocnych elementów znacznie usprawni programowanie na platformie Windows.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_40_/g_-_-x-_-_-_x20170112003503_0.jpg)





## UWP Community Toolkit - niezbędnik dewelopera

 
Pomimo rozbudowanego SDK pod UWP (a jednocześnie ograniczonego, niestety) gigant z Redmond postanowił zebrać w jednym miejscu wszystkie dodatki, jakie mogą przydać się przy tworzeniu aplikacji. Znajdziemy tu zarówno rozwiązania pracowników giganta z Redmond jak i biblioteki, które wcześniej tworzone były przez niezależnych pasjonatów.Tak właśnie powstał UWP Community Toolkit, który rozwijany jest przez Microsoft ze społecznością deweloperów. 


Projekt jest całkowicie darmowy, a jego źródła wrzucone są na [GitHuba](https://github.com/Microsoft/UWPCommunityToolkit).  UWP Community Toolkit podzielono na kilka bibliotek, które dołączmy szybko do projektu poprzez [Nugeta](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/)  wpisując  *Microsoft.Toolkit.UWP* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_40_/g_-_-x-_-_-_x20170112003325_0.png)



W celu dodania pakietu do istniejącego projektu należy pamiętać, iż projekt UWP musi być kompatybilny  z Windows SDK co najmniej w wersji 10586. Toolkit współgra z całą platformą bazującą na Windows 10 czyli PC, Mobile, XBOX, IoT i HoloLens. Microsoft postarał się także, aby udostępnić całkiem  wyczerpującą [dokumentację](http://docs.uwpcommunitytoolkit.com/en/master/).  Zestaw może być użyty zarówno przez osoby piszące w C# jak i VB.NET (też jest coś do JS).

Aktualna wersja nosi numerek 1.2, a w lutym planowane jest wydanie wersji 1.3 z poprawkami błędów, nowymi kontrolkami czy obsługa OneDrive.



## Co w zestawie?



Toolkit został podzielony na kilka paczek:




  * Microsoft.Toolkit.Uwp - główna biblioteka z niezbędnymi dodatkami, zawiera ułatwienia przy używaniu Storage, Http response/request, wykrywaniu sieci/Internetu itd.


  * Microsoft.Toolkit.Uwp.Notifications - paczka wspomagająca tworzenie powiadomień toast i żywych kafelków 


  * Microsoft.Toolkit.Uwp.Notifications.Javascript - paczka jak wyżej, ale pod JS


  * Microsoft.Toolkit.Uwp.Services - obsługa zewnętrznych serwisów Bing, Facebook, LinkedIn, Microsoft Graph oraz Twitter


  * Microsoft.Toolkit.Uwp.UI - biblioteka oferuje zestaw dodatków do UI w XAML, jak np. gotowy zbiór konwerterów czy wyszukiwanie po drzewie XAML 


  * Microsoft.Toolkit.Uwp.UI.Animations - zbiór animacji


  * Microsoft.Toolkit.Uwp.UI.Controls - 16 nowych kontrolek, które rozszerzają dostępne kontroli XAML z SDK, jak np. HamburgerMenu, AdaptiveGridView czy MasterDetailsView 






![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_40_/g_-_-x-_-_-_x20170110235223_0.png)

 

Trzeba przyznać, że jest tego całkiem sporo i ciężko jest do czegoś się przyczepić. W razie jeśli gotowy kod nie spełnia naszych oczekiwać możne go zmienić/rozszerzyć bazując na kodzie źródłowym.

Poszczególne dodatki nie są niczym rewolucyjnym, ale pozwalają na efektywniejsze tworzenie aplikacji na platformę UWP. Sprawdźmy szybko dwa przykłady.

Weźmy pod lupę kontrolkę HamburgerMenu z toolkitu. Jest ona niczym innym jak znacznie [rozszerzoną wersją standardowej kontrolki SplitView](https://github.com/Microsoft/UWPCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Controls/HamburgerMenu/HamburgerMenu.xaml)  z SDK. Niby nic wielkiego, ale o ile przyspieszy zbudowanie aplikacji bazującej na  *menu z hamburgerem* .



Podobnie jest z helperem do powiadomień toast. Standardowo, aby wyświetlić powiadomienie musimy przekazać do metody XMLa. Zatem aby pokazać powiadomienie z przypomnieniem:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_40_/g_-_-x-_-_-_x20170112000715_0.PNG)



Do metody należy dostarczyć taki oto XML:



```html

<toast launch="action=viewEvent&amp;eventId=1983" scenario="reminder">
  
  <visual>
    <binding template="ToastGeneric">
      <text>Adaptive Tiles Meeting</text>
      <text>Conf Room 2001 / Building 135</text>
      <text>10:00 AM - 10:30 AM</text>
    </binding>
  </visual>

  <actions>
    
    <input id="snoozeTime" type="selection" defaultInput="15">
      <selection id="1" content="1 minute"/>
      <selection id="15" content="15 minutes"/>
      <selection id="60" content="1 hour"/>
      <selection id="240" content="4 hours"/>
      <selection id="1440" content="1 day"/>
    </input>

    <action
      activationType="system"
      arguments="snooze"
      hint-inputId="snoozeTime"
      content=""/>

    <action
      activationType="system"
      arguments="dismiss"
      content=""/>
    
  </actions>
  
</toast>

```



Niby nic wielkiego, ale musimy usiąść z dokumentacją i "ręcznie" stworzyć takiego XMLa, jednocześnie zapominając o intellisense czy walidacji błędów podczas pisania.

W tym przypadku z pomocą przyjdzie nam UWP Community Toolkit. Pakiet dostarczy odpowiednią strukturę klas, która będzie w stanie wygenerować na jej podstawie XMLa:



```csharp

var xml = new ToastContent()
    {
        Launch = "action=viewEvent&eventId=1983",
        Scenario = ToastScenario.Reminder,

        Visual = new ToastVisual()
        {
            BindingGeneric = new ToastBindingGeneric()
            {
                Children =
                {
                    new AdaptiveText()
                    {
                        Text = "Adaptive Tiles Meeting"
                    },

                    new AdaptiveText()
                    {
                        Text = "Conf Room 2001 / Building 135"
                    },

                    new AdaptiveText()
                    {
                        Text = "10:00 AM - 10:30 AM"
                    }
                }
            }
        },

        Actions = new ToastActionsCustom()
        {
            Inputs =
            {
                new ToastSelectionBox("snoozeTime")
                {
                    DefaultSelectionBoxItemId = "15",
                    Items =
                    {
                        new ToastSelectionBoxItem("1", "1 minute"),
                        new ToastSelectionBoxItem("15", "15 minutes"),
                        new ToastSelectionBoxItem("60", "1 hour"),
                        new ToastSelectionBoxItem("240", "4 hours"),
                        new ToastSelectionBoxItem("1440", "1 day")
                    }
                }
            },

            Buttons =
            {
                new ToastButtonSnooze()
                {
                    SelectionBoxId = "snoozeTime"
                },

                new ToastButtonDismiss()
            }
        }
    }.GetXml();


```



Szybko i praktycznie bez zaglądania do dokumentacji, stworzymy podstawowe powiadomienie. Można zastanowić się, dlaczego takie rozwiązanie nie jest standardowo udostępnione w SDK.

Warto dodać, że wykorzystanie biblioteki jest niezmiernie proste i przyjemne, a to dzięki...



## UWP Community Toolkit Sample App


Świetnym dodatkiem do omawianego pakietu jest aplikacja UWP Community Toolkit Sample App dostępna w [markecie Windows](https://www.microsoft.com/pl-pl/store/p/uwp-community-toolkit-sample-app/9nblggh4tlcq).  Warto ją pobrać, aby na żywo przetestować jak działają poszczególne elementy. Sprawdzimy działanie kontrolek, notyfikacji czy helperów. Dodatkowo z działającym przykładem umieszczony jest obok kod, który odpowiada za przedstawioną funkcjonalność.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_40_/g_-_-x-_-_-_x20170111001453_0.png)




Pakiet UWP Community Toolkit będzie idealnym wyborem dla osób rozpoczynających przygodę z UWP, jak i dla tych, którzy są już zaznajomieni z tematem. Pierwsi zyskają szybki start do nowej platformy, drudzy również przyspieszą deweloping, a dodatkowo odnajdą kilka ciekawych rozwiązań do wykorzystania we własnych implementacjach.

Cały toolkit jest niezmiernie ciekawy, a w kilku przypadkach można się zastanowić dlaczego dane elementy nie są standardowo wbudowane w SDK.
