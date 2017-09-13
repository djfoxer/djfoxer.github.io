---layout:     post
title:      UWP Community Toolkit — niezbędnik dewelopera Universal Windows Platform
date:       2017-01-12 17:26:00
summary:    Tworzenie aplikacji na najświeższą platformę Windows (Universal Windows Platform) nie powinno sprawiać dużych problemów nawet początkującym osobom w tym temacie. Warto jednak już od pierwszych kroków wyposażyć się w ciekawy zbiór bibliotek od Microsoftu, który uprzyjemni pracę w UWP. Zróżnicowany ze...
categories: windows porady programowanie
---



Tworzenie aplikacji na najświeższą platformę Windows (Universal Windows Platform) nie powinno sprawiać dużych problemów nawet początkującym osobom w tym temacie. Warto jednak już od pierwszych kroków wyposażyć się w ciekawy zbiór bibliotek od Microsoftu, który uprzyjemni pracę w UWP. Zróżnicowany zestaw pomocnych elementów znacznie usprawni programowanie na platformie Windows.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_26_/g_-_608x405_-_-_78412x20170112003503_0.jpg





## UWP Community Toolkit - niezbędnik dewelopera

 
Pomimo rozbudowanego SDK pod UWP (a jednocześnie ograniczonego, niestety) gigant z Redmond postanowił zebrać w jednym miejscu wszystkie dodatki, jakie mogą przydać się przy tworzeniu aplikacji. Znajdziemy tu zarówno rozwiązania pracowników giganta z Redmond jak i biblioteki, które wcześniej tworzone były przez niezależnych pasjonatów.Tak właśnie powstał UWP Community Toolkit, który rozwijany jest przez Microsoft ze społecznością deweloperów. 


Projekt jest całkowicie darmowy, a jego źródła wrzucone są na [GitHuba](https://github.com/Microsoft/UWPCommunityToolkit). UWP Community Toolkit podzielono na kilka bibliotek, które dołączmy szybko do projektu poprzez [Nugeta](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/) wpisując  *Microsoft.Toolkit.UWP* .

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_26_/g_-_608x405_-_-_78412x20170112003325_0.png



W celu dodania pakietu do istniejącego projektu należy pamiętać, iż projekt UWP musi być kompatybilny  z Windows SDK co najmniej w wersji 10586. Toolkit współgra z całą platformą bazującą na Windows 10 czyli PC, Mobile, XBOX, IoT i HoloLens. Microsoft postarał się także, aby udostępnić całkiem  wyczerpującą [dokumentację](http://docs.uwpcommunitytoolkit.com/en/master/). Zestaw może być użyty zarówno przez osoby piszące w C# jak i VB.NET (też jest coś do JS).

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




)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_26_/g_-_608x405_-_-_78412x20170110235223_0.png

 

Trzeba przyznać, że jest tego całkiem sporo i ciężko jest do czegoś się przyczepić. W razie jeśli gotowy kod nie spełnia naszych oczekiwać możne go zmienić/rozszerzyć bazując na kodzie źródłowym.

Poszczególne dodatki nie są niczym rewolucyjnym, ale pozwalają na efektywniejsze tworzenie aplikacji na platformę UWP. Sprawdźmy szybko dwa przykłady.

Weźmy pod lupę kontrolkę HamburgerMenu z toolkitu. Jest ona niczym innym jak znacznie [rozszerzoną wersją standardowej kontrolki SplitView](https://github.com/Microsoft/UWPCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Controls/HamburgerMenu/HamburgerMenu.xaml) z SDK. Niby nic wielkiego, ale o ile przyspieszy zbudowanie aplikacji bazującej na  *menu z hamburgerem* .



Podobnie jest z helperem do powiadomień toast. Standardowo, aby wyświetlić powiadomienie musimy przekazać do metody XMLa. Zatem aby pokazać powiadomienie z przypomnieniem:

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_26_/g_-_608x405_-_-_78412x20170112000715_0.PNG



Do metody należy dostarczyć taki oto XML:


```html

&lt;toast launch=&quot;action=viewEvent&amp;amp;eventId=1983&quot; scenario=&quot;reminder&quot;&gt;
  
  &lt;visual&gt;
    &lt;binding template=&quot;ToastGeneric&quot;&gt;
      &lt;text&gt;Adaptive Tiles Meeting&lt;/text&gt;
      &lt;text&gt;Conf Room 2001 / Building 135&lt;/text&gt;
      &lt;text&gt;10:00 AM - 10:30 AM&lt;/text&gt;
    &lt;/binding&gt;
  &lt;/visual&gt;

  &lt;actions&gt;
    
    &lt;input id=&quot;snoozeTime&quot; type=&quot;selection&quot; defaultInput=&quot;15&quot;&gt;
      &lt;selection id=&quot;1&quot; content=&quot;1 minute&quot;/&gt;
      &lt;selection id=&quot;15&quot; content=&quot;15 minutes&quot;/&gt;
      &lt;selection id=&quot;60&quot; content=&quot;1 hour&quot;/&gt;
      &lt;selection id=&quot;240&quot; content=&quot;4 hours&quot;/&gt;
      &lt;selection id=&quot;1440&quot; content=&quot;1 day&quot;/&gt;
    &lt;/input&gt;

    &lt;action
      activationType=&quot;system&quot;
      arguments=&quot;snooze&quot;
      hint-inputId=&quot;snoozeTime&quot;
      content=&quot;&quot;/&gt;

    &lt;action
      activationType=&quot;system&quot;
      arguments=&quot;dismiss&quot;
      content=&quot;&quot;/&gt;
    
  &lt;/actions&gt;
  
&lt;/toast&gt;

```


Niby nic wielkiego, ale musimy usiąść z dokumentacją i &quot;ręcznie&quot; stworzyć takiego XMLa, jednocześnie zapominając o intellisense czy walidacji błędów podczas pisania.

W tym przypadku z pomocą przyjdzie nam UWP Community Toolkit. Pakiet dostarczy odpowiednią strukturę klas, która będzie w stanie wygenerować na jej podstawie XMLa:


```csharp

var xml = new ToastContent()
    {
        Launch = &quot;action=viewEvent&amp;eventId=1983&quot;,
        Scenario = ToastScenario.Reminder,

        Visual = new ToastVisual()
        {
            BindingGeneric = new ToastBindingGeneric()
            {
                Children =
                {
                    new AdaptiveText()
                    {
                        Text = &quot;Adaptive Tiles Meeting&quot;
                    },

                    new AdaptiveText()
                    {
                        Text = &quot;Conf Room 2001 / Building 135&quot;
                    },

                    new AdaptiveText()
                    {
                        Text = &quot;10:00 AM - 10:30 AM&quot;
                    }
                }
            }
        },

        Actions = new ToastActionsCustom()
        {
            Inputs =
            {
                new ToastSelectionBox(&quot;snoozeTime&quot;)
                {
                    DefaultSelectionBoxItemId = &quot;15&quot;,
                    Items =
                    {
                        new ToastSelectionBoxItem(&quot;1&quot;, &quot;1 minute&quot;),
                        new ToastSelectionBoxItem(&quot;15&quot;, &quot;15 minutes&quot;),
                        new ToastSelectionBoxItem(&quot;60&quot;, &quot;1 hour&quot;),
                        new ToastSelectionBoxItem(&quot;240&quot;, &quot;4 hours&quot;),
                        new ToastSelectionBoxItem(&quot;1440&quot;, &quot;1 day&quot;)
                    }
                }
            },

            Buttons =
            {
                new ToastButtonSnooze()
                {
                    SelectionBoxId = &quot;snoozeTime&quot;
                },

                new ToastButtonDismiss()
            }
        }
    }.GetXml();


```


Szybko i praktycznie bez zaglądania do dokumentacji, stworzymy podstawowe powiadomienie. Można zastanowić się, dlaczego takie rozwiązanie nie jest standardowo udostępnione w SDK.

Warto dodać, że wykorzystanie biblioteki jest niezmiernie proste i przyjemne, a to dzięki...



## UWP Community Toolkit Sample App


Świetnym dodatkiem do omawianego pakietu jest aplikacja UWP Community Toolkit Sample App dostępna w [markecie Windows](https://www.microsoft.com/pl-pl/store/p/uwp-community-toolkit-sample-app/9nblggh4tlcq). Warto ją pobrać, aby na żywo przetestować jak działają poszczególne elementy. Sprawdzimy działanie kontrolek, notyfikacji czy helperów. Dodatkowo z działającym przykładem umieszczony jest obok kod, który odpowiada za przedstawioną funkcjonalność.

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-1-12-_26_/g_-_608x405_-_-_78412x20170111001453_0.png




Pakiet UWP Community Toolkit będzie idealnym wyborem dla osób rozpoczynających przygodę z UWP, jak i dla tych, którzy są już zaznajomieni z tematem. Pierwsi zyskają szybki start do nowej platformy, drudzy również przyspieszą deweloping, a dodatkowo odnajdą kilka ciekawych rozwiązań do wykorzystania we własnych implementacjach.

Cały toolkit jest niezmiernie ciekawy, a w kilku przypadkach można się zastanowić dlaczego dane elementy nie są standardowo wbudowane w SDK.
)