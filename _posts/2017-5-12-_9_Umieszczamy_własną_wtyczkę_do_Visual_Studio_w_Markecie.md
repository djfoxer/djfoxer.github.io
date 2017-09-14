---
layout:     post
title:      Umieszczamy własną wtyczkę do Visual Studio w Markecie
date:       2017-05-12 23:23:00
summary:    Nareszcie udało mi się znaleźć chwilę wolnego po tym całym ślubnym zamieszaniu ;) Wtyczka do Visual Studio monitorująca czas i zdrowie dewelopera już coś zaczyna sobą reprezentować. Postanowiłem zatem dodać rozszerzenie do marketu, aby każdy mógł  zainstalować ją w swoim IDE i zgłosić wszelakie błędy i uwagi. W tym poradniku przedstawię sposób na umieszczenie wtyczki do Visual Studio w Markecie. P...
categories: windows oprogramowanie programowanie
---



Nareszcie udało mi się znaleźć chwilę wolnego po tym całym ślubnym zamieszaniu ;) Wtyczka do Visual Studio monitorująca czas i zdrowie dewelopera już coś zaczyna sobą reprezentować. Postanowiłem zatem dodać rozszerzenie do marketu, aby każdy mógł  zainstalować ją w swoim IDE i zgłosić wszelakie błędy i uwagi. W tym poradniku przedstawię sposób na umieszczenie wtyczki do Visual Studio w Markecie. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512231128_0.PNG)



## Przygotowanie pliku manifest

Przygodę zaczynamy od otworzenia pliku  *source.extension.vsixmanifest* . To w nim znajdują się szczegóły, które będą wyświetlane na ekranie dodatku w markecie. Na pierwszej zakładce  *Metadata*  można uzupełnić opis, domyślną ikonę czy tagi.   


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224740_0.png)


Kolejna,  *Install Targets* , opisuje jakie wersję Visual Studio będą wspierane. Podajemy tutaj nie tylko wersję numeryczną, ale również wersję funkcjonalną. W moim przypadku są to wydania Visual Studio Community, Pro i Enterprise w wersjach 2015 i wyższe.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224737_1.png)


W oknie  *Dependencies*  można określić jakie zależności i w jakich wersjach są wymagane do zainstalowania wtyczki.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224740_2.png)


Ostatnia zakładka określa jakie elementy i w jakich wersjach powinny znajdować się w zainstalowanej wersji IDE, do której będzie instalowany dodatek.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224740_3.png)


Po uzupełnieniu pól buildujemy projekt w trybie  *Release*  i w folderze  *\bin\Release*  otrzymamy gotowy instalator VSIX z naszą wtyczką.


## Dodanie wtyczki do Marketu


Mając już plik VSIX możemy przystąpić do umieszczenia dodatku w Markecie Visual Studio. W tym celu przechodzimy na stronę [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) i klikamy na [Upload](https://visualstudiogallery.msdn.microsoft.com/site/upload/view).

Cały proces trwa bardzo szybko i jest on przeprowadzany za pomocą kreatora. W pierwszej kolejności wybieramy typ naszej wtyczki:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224737_0.png)


Następnie zaznaczmy chęć wrzucenia dodatku z dysku, po czym wybieramy stworzony przed chwilą plik VSIX z rozszerzeniem. Po zaczytaniu dodatku ujrzymy okienko z informacjami o naszym pluginie.

Są tutaj informacje o nazwie, wersji, opisie, ikonie, a także tagach i kategoriach.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224741_2.png)


Z pliku odczytane są również wspierane wersje IDE i język. To tutaj umieścimy informację o tym czy wtyczka jest płatna, a także link do kodu źródłowego.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224741_3.png)


Na samym dole umieszczono prosty edytor WYSIWYG do stworzenia szczegółowego opisu naszej wtyczki.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224741_4.png)


Po uzupełnieniu pól  zapisujemy nasze dane. W tym momencie zostaniemy przekierowani na stronę z podsumowaniem dotychczasowych prac. Wystarczy już tylko kliknąć na przycisk  *Publish* , aby umieścić rozszerzenie w Markecie. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512232058_0.png)


Po chwili będzie ono dostępne dla każdego użytkownika Visual Studio.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512232058_1.png)



## Healthy With VS w Markecie

Wraz z tym tutorialem umieściłem bardzo wczesną wersję dodatku w Markecie. Jak pamiętacie [Healthy With VS](https://www.dobreprogramy.pl/djfoxer/Healthy-with-Visual-Studio-Daj-Sie-Poznac,s308.html) jest pluginem tworzonym na konkurs Daj Się Poznać 2017.  Zachęcam do instalacji i zgłaszania uwag. Obecnie dodatek wyświetla Timer Pomodoro na pasku statusu, a na koniec odliczania uruchamia dźwięk i 20 sekundowe slajdy przedstawiające ćwiczenia rozciągające. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512231344_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512231402_0.png)



> Dodatek dostępny jest w markecie pod adresem: [Healthy With VS](https://marketplace.visualstudio.com/items?itemName=djfoxer.HealthyWithVS).


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512224730_0.PNG)


Zachęcam do pobierania i testowania pierwszej wersji. Liczę również na feedback z waszej strony.



> Źródła dostępne są na GitHubie (branch master i POC):
> [https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-12-_9_/g_-_608x405_-_-_81008x20170512231640_0.png)

 