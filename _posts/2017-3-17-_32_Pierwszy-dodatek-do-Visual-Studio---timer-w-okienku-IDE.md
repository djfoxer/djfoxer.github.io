---
layout:     post
title:      Pierwszy dodatek do Visual Studio — timer w okienku IDE
date:       2017-03-17 17:06:00
summary:    Przyszedł czas na mięsko. W tym wpisie przedstawię sposób na stworzenie wtyczki do Visual Studio, która będzie timerem odliczającym 25 minut w dół (technika Pomodoro ).Stworzony dodatek będzie pływającym okienkiem, które będzie można przypiąć w dowolne miejsce w ekranie roboczym Visual Studio.<!----><!---->Zaczynamy!Tworzymy projekt!Pierwsze kroki zaczynamy od stworzenia nowego projektu VSIX Proje...
categories: windows oprogramowanie programowanie
slug: Pierwszy-dodatek-do-Visual-Studio-timer-w-okienku-IDE,79926.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225241_0.PNG
---



Przyszedł czas  *na mięsko* . W tym wpisie przedstawię sposób na stworzenie wtyczki do Visual Studio, która będzie timerem odliczającym 25 minut w dół ([technika Pomodoro](http://blog.djfoxer.pl/Technika-Pomodoro-efektywne-zarzadzanie-czasem-pracy,79724.html) ).

Stworzony dodatek będzie pływającym okienkiem, które będzie można przypiąć w dowolne miejsce w ekranie roboczym Visual Studio.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225241_0.PNG)



Zaczynamy!



## Tworzymy projekt!



Pierwsze kroki zaczynamy od stworzenia nowego projektu VSIX Project. Jest to podstawowy szablon używany przy budowaniu rozszerzeń do Visual Studio.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225240_0.PNG)




Na początku dostaniemy pusty projekt z plikiem  *source.extension.vsixmanifest* . 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225240_1.PNG)



W tym miejscu ustalamy wszelakie opcje odnośnie tworzonej wtyczki. Wybierzemy zatem wersje Visual Studio, na jakie można będzie zainstalować tworzony plugin, wymagane biblioteki w systemie użytkownika czy opis i ikony dodatku.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316230424_0.PNG)



Teraz dodajmy nowy plik do projektu: Custom Tool Window.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225240_2.PNG)



W ten sposób Visual Studio przygotuje gotowe okno, które można będzie dostosować do własnych  potrzeb. Dostaniemy kilka plików, które warto omówić. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225240_3.PNG)



 *TimerToolWindowPackage.vsct*  zawiera opis tego, gdzie w Visual Studio ma się pojawić odnośnik do naszego okna.



```html

      <Button guid="guidTimerToolWindowPackageCmdSet" id="TimerToolWindowCommandId"
        priority="0x0100" type="Button">
        <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
          <ButtonText>TimerToolWindow</ButtonText>
        </Strings>
      </Button>
    </Buttons>

```



Powyższy kod umiejscawia przycisk (button) w menu Other Windows ( *<Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>* ).

Elementy do naszego okna są grupowane w  *paczkę* , która zawiera niezbędne klasy odpowiadające za inicjalizację i ustawienie wszelakich opcji. Na tym etapie stworzone przez Visual Studio pliki wystarczą nam w zupełności. Przejdźmy jednak do pliku  *TimerToolWindowControl.xaml* , który jest zwykłym widokiem xaml.




## Budujemy okienko narzędziowe

 

W tym momencie osoby mające styczność z WPFem będą się czuły jak w domu. Tworzymy i oprogramowujemy widok, który będzie zawarty w pływającym oknie. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316232924_0.PNG)



Widok będzie jak najbardziej prosty jak tylko można. Trzy przyciski i timer odliczający 25 minut w dół. Kiedy zegar dojdzie do końca (00 : 00) tło zmienia kolor na czerwony i tyle. Można będzie rozpocząć odliczanie, zatrzymać i wyczyścić. 

Kod nie będzie również specjalnie wymyślny, tak aby był jak najprostszy.  *DispatcherTimer*  będzie odpowiadał za odświeżanie timer co 1 sekundę i pokazywanie pozostałego czasu.




```csharp

        DispatcherTimer disTimer = new DispatcherTimer();
        uint seconds = 0;
        uint maxSeconds = 1500;

        /// <summary>
        /// Initializes a new instance of the <see cref="TimerToolWindowControl"/> class.
        /// </summary>
        public TimerToolWindowControl()
        {
            this.InitializeComponent();
            DataContext = this;
            disTimer.Interval = TimeSpan.FromSeconds(1);
            disTimer.Tick += DisTimer_Tick;
            seconds = maxSeconds;
            BackgroundColor = Brushes.Black;
            SetTimerText();
        }

        private void DisTimer_Tick(object sender, System.EventArgs e)
        {
            if (seconds <= 0)
            {
                disTimer.Stop();
                BackgroundColor = Brushes.Red;
            }
            else
            {
                seconds--;
            }
            SetTimerText();
        }

        private void Button_Click_start(object sender, RoutedEventArgs e)
        {
            disTimer.Start();
            BackgroundColor = Brushes.Black;
        }

        private void Button_Click_stop(object sender, RoutedEventArgs e)
        {
            disTimer.Stop();
        }

        private void Button_Click_clear(object sender, RoutedEventArgs e)
        {
            seconds = maxSeconds;
            SetTimerText();
            disTimer.Stop();
            BackgroundColor = Brushes.Black;
        }

        private void SetTimerText()
        {
            SecondsText = ((seconds - (seconds % 60)) / 60).ToString("D2") + " : " + (seconds % 60).ToString("D2");
        }

```





## Sprawdźmy naszą wtyczkę w działaniu


Przyszedł czas na debugowanie. Odpalamy projekt, który otworzy specjalną instancję Visual Studio. Wybieramy z menu View, Other Windows i nasze utworzone okno  *TimerToolWindow* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225317_0.PNG)



Otwarte okienko można umieścić w dowolnym miejscu IDE. Jak przypiąłem ją na dole, pod Solution Explorerem. 




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225316_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316225240_4.PNG)



Podstawowe rzeczy jakie możemy stworzyć do wtyczki nie są skomplikowane. Na [Githubie](https://github.com/Microsoft/VSSDK-Extensibility-Samples)  od Microsoftu znajdziemy wiele przykładowych gotowych pluginów, które idealnie nadadzą się do rozpoczęcia prac nad własnymi dodatkami do Visual Studio. Warto przejrzeć kod i podpatrzeć jak pewne rzeczy można wykonać. Oczywiście im dalej w las tym ciemniej. Bardziej customowe rzeczy i większe funkcjonalności wymagają już szerszej wiedzy. W kolejnych przykładach będą kolejne elementy, które przydadzą się do stworzenia finalnej wtyczki Healthy with Visual Studio na konkurs.





> Źródła dostępne są na GitHubie (branch master i POC):
> [https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-17-_32_/g_-_-x-_-_-_x20170316235741_0.png)


