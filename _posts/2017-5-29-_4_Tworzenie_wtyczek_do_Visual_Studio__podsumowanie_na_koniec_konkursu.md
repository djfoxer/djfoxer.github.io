---
layout:     post
title:      Tworzenie wtyczek do Visual Studio: podsumowanie na koniec konkursu
date:       2017-05-29 19:36:00
summary:    Właśnie stuknął 20. wpis w konkursie Daj Się Poznać 2017, zatem przyszedł czas na podsumowanie prac na koniec trwania trzymiesięcznych zmagań...Statystycznie W tym czasie wpisy miały sumarycznie prawie 42 tysiące wyświetleń. Najbardziej obleganym wpisem był ten o hakowaniu Visual Studio, czyli o dob...
categories: windows porady programowanie
---



Właśnie stuknął 20. wpis w konkursie Daj Się Poznać 2017, zatem przyszedł czas na podsumowanie prac na koniec trwania trzymiesięcznych zmagań...



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529185905_0.png)





### Statystycznie

 

W tym czasie wpisy miały sumarycznie prawie 42 tysiące wyświetleń. Najbardziej obleganym wpisem był ten o [hakowaniu Visual Studio](https://www.dobreprogramy.pl/djfoxer/Hakujemy-Visual-Studio-dobieramy-sie-do-niedostepnych-elementow-IDE,80126.html), czyli o dobieraniu się bezpośrednio do poszczególnych elementów UI poprzez Snoopa. Niemalże identyczną ilość wyświetleń ma wpis odnośnie aplikacji (i nie tylko) wspomagających zdrową pracę przy komputerze: [Zdrowe ciało, zdrowy duch, zdrowy programista — przegląd aplikacji](https://www.dobreprogramy.pl/djfoxer/Zdrowe-cialo-zdrowy-duch-zdrowy-programista-przeglad-aplikacji,79589.html). Oczywiście wszystkie wpisy dostępne są[ pod linkiem](https://www.dobreprogramy.pl/djfoxer/Healthy-with-Visual-Studio-Daj-Sie-Poznac,s308.html) grupującym moje artykuły.



### Projekt - Healthy With VS


Głównym celem prac konkursowych było stworzenie dodatku do Visual Studio, który wspomagałby czas pracy i dbał jednocześnie o zdrowie programisty. Finalnie udało się stworzyć plugin, który implementuje timer Pomodoro w pasku statusu IDE. Dodatkowo można ustawić, aby na koniec pracy ekran(y) były blokowane przez plansze przedstawiające ćwiczenia rozciągające, idealne dla osób siedzących sporo przy komputerze.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529185915_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529185915_0.jpg)



Oczywiście dodatek znajduje się w Markecie pluginów do Visual Studio i każdy może go pobrać i przetestować:

<blockquote>
<p>link: [Healthy With VS](https://marketplace.visualstudio.com/items?itemName=djfoxer.HealthyWithVS)
</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529185915_1.PNG)



Pełne źródła pluginu znajdują się na [GitHubie](https://github.com/djfoxer/healthyWithVS).




### Projekt - Bad Word Detector


Tuż przed zamknięciem konkursu wpadł mi do głowy pomysł na jeszcze jeden dodatek do IDE. Otóż wiele mówi się ostatnio o wpadkach programistów, którzy zostawili w kodzie wszelkiego rodzaju komentarze ze słowami, które nie do końca powinny znaleźć się w wersji finalnej dla klienta. Nie oszukujmy się, każdy z nas czasem w ramach testów napisze komentarz czy zmienną "dupa" lub "fuck", ale zgodzimy się, że na produkcji takie rzeczy nie powinny mieć miejsca. W tym momencie do akcji wkracza dodatek Bad Word Detector. Plugin, który w otwartym pliku w edytorze Visual Studio zaznaczy wulgarne słowa.

Obecnie extension wykrywa słowa w języku angielskim, ale niedługo dodam listę wulgaryzmów w naszej ojczystej mowie, a także możliwość sprawdzenia wszystkich plików w solucji za pomocą jednego kliknięcia.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529190842_0.PNG)



Bad Word Detector również znajduje się w Markecie Visual Studio i można już go pobrać i samemu sprawdzić jak działa:

<blockquote>
<p>link: [Bad Word Detector](https://marketplace.visualstudio.com/items?itemName=djfoxer.BadWordDetector-18879)
</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529185915_2.PNG)



Pełne źródła pluginu znajdują się na [GitHubie](https://github.com/djfoxer/bad-word-detector).




### Merytorycznie


Dodatkowo z wpisów można było dowiedzieć się odnośnie tego, jak  zacząć przygodę z tworzeniem dodatków do VS, czym jest MEF, na co pozwala Visual Studio SDK, jak dodać opcje konfiguracyjne do wtyczki, aktywować zapis do loga czy jak dobrać się do niedostępnych elementów IDE. Dodatkowo można było przeczytać tutorial o dodawaniu dodatku do Marketu, a także szybkim tworzeniu postaci ludzkich w 3D i migrowaniu starych projektów stworzonych w VS 2015 do najnowszej wersji. Sporo było o zdrwej pracy przy komputerze i technice Pomodoro. Przy okazji pojawił się wpis o konferencji 4Developers i dodatku do VS od Microsoftu: Windows Template Studio. Wszystkie wpisy zebrane są pod [linkiem](https://www.dobreprogramy.pl/djfoxer/Healthy-with-Visual-Studio-Daj-Sie-Poznac,s308.html).

Prócz  *fizycznych*  dodatków w Markecie powstało sporo ciekawych wpisów, które zapewne okażą się przydatne dla wielu osób. Same dodatki będą rozwijane, w szczególności... Bad Word Detector, który ma spory potencjał na rozwój i szersze zastosowanie :)


### Na koniec..


Konkurs już się niemalże zakończył. Mam nadzieję, że powstałe wpisy będę chętnie odwiedzane, a dodatki znajdą swoje miejsce w wielu instancjach VS :) Miło było uczestniczyć w evencie, jakim jest konkurs Daj Się Poznać, ale przyszedł czas na zamknięcie edycji 2017. Mam nadzieję, że gdzieś tam projekt konkursowy zostanie chociaż w małym stopniu zauważony i zbierze przychylne opinie. Miłego :)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-29-_4_/g_-_608x405_-_-_81326x20170529192401_0.jpg)

