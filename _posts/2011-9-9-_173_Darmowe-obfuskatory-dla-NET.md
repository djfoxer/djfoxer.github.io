---
layout:     post
title:      Darmowe obfuskatory dla .NET
date:       2011-09-09 00:14:00
summary:    Obfuskacja (zaciemnianie kodu) jest techniką mającą na celu, takie przekształcenie kodu, aby jego odczytanie było maksymalnie utrudnione. Jednocześnie transformacja nie może zakłócić działania programu.Technika jest użyteczna, w przypadkach gdy chcemy zapobiec, utrudnić analizę kodu programu. Jest to niezwykle ważne dla aplikacji pisanych w językach, których wynikowe programy są w postaci kodu poś...
categories: windows oprogramowanie programowanie
slug: Darmowe-obfuskatory-dla-.NET,27654.html
---



Obfuskacja (zaciemnianie kodu) jest techniką mającą na celu, takie przekształcenie kodu, aby jego odczytanie było maksymalnie utrudnione. Jednocześnie transformacja nie może zakłócić działania programu.

Technika jest użyteczna, w przypadkach gdy chcemy zapobiec, utrudnić analizę kodu programu. Jest to niezwykle ważne dla aplikacji pisanych w językach, których wynikowe programy są w postaci kodu pośredniego, interpretowanego bezpośrednio na maszynie klienckiej (C#, Java).

Obfuskacja nie daje 100% bezpieczeństwa. Jej celem jest maksymalne utrudnienie inżynierii wstecznej, dokładnej analizy programu.

Najczęściej aplikacje do obfuskacji zaciemniają kod poprzez: 
- zmianę układu: zmiana nazw zmiennych, formatowania (spacje, znaki specjalne) itp.
- zmianę danych: odseparowanie zmiennych, zmiana długości życia zmiennej
- zmiana kontroli: zmiana przebiegu, dodatkowe warunki dla pętli, wstawienie wyrażeń, metod nie wpływający na ogólną pracę aplikacji

Przykład działania obfuskatorów:

Oryginalny kod przed kompilacją:

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-9-9-_173_/g_-_608x405_-_-_27654x20110908182452_1.png)
 
 
Kod uzyskany z pliku exe, poprzez dekompilację:

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-9-9-_173_/g_-_608x405_-_-_27654x20110908182452_2.png)
 

Kod uzyskany z pliku exe (z obfuskacją), poprzez dekompilację:

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-9-9-_173_/g_-_608x405_-_-_27654x20110908182452_3.png)
 

Z racji tego, iż obfuskatory są narzędziami niezbędnymi w pracy developerów, ich ceny nie są małe. Wahają się od 100$ do ponad 1000$ (albo i duużo więcej) za jedno stanowisko. 

Spróbowałem poszukać darmowych rozwiązań dla technologi .NET, które w warunkach domowych lub małych firm, mogą przez początkowy okres działalności, zastąpić płatne wersje. Oto co udało mi się znaleźć:


## Eazfuscator.NET


[http://eazfuscator.net](http://eazfuscator.net)
Bardzo proste w obsłudze narzędzie (przeciągnij i upuść). Aplikacja używa wielu metod obfuskacji i można zastosować ją do większości projektów .NET. Niestety nie obsługuje bardziej zagnieżdżonych crossreferencji. Mimo wszystko polecam na początek!


## Skater .NET Obfuscator Freeware Light Edition


[http://www.rustemsoft.com/freeware_obfuscator.htm](http://www.rustemsoft.com/freeware_obfuscator.htm)
Biedniejsza, ograniczona, wersja aplikacji płatnej. Dużo opcji odnośnie obfuskacji. Czasem używam, gdy  Eazfuscator.NET nie daje sobie rady z crossreferencjami.


## CodeFort Free Edition


[http://codefort.org/download](http://codefort.org/download)
Darmowa, ograniczona wersja w stosunku do płatnej Professional. Szybka i bez zbędnych rozbudowanych opcji. Używam w trudnych sytuacjach, gdy Eazfuscator.NET odmawia posłuszeństwa.


## Dotfuscator Community Edition


[http://www.preemptive.com/products/dotfuscator/compare-editions
](http://www.preemptive.com/products/dotfuscator/compare-editions)Dostarczony z wyższymi wersjami Visual Studio. Uboższa wersja Dotfuscator Professional Edition.


## Phoenix Protector


[http://ntcore.com/phoenix.php](http://ntcore.com/phoenix.php)
Ciekawa aplikacja. Prosta w obsłudze. Podobno wynikowy kod nie jest specjalnie wymyślny. Nie testowałem dłużej, nie wiem czemu nie mogłem się do niej przekonać, może ze względu na to, iż Eazfuscator.NET wydał mi się lepszy.


## Assemblur


[http://www.metapropeller.com/](http://www.metapropeller.com/)
Obfuskuje zarówno kod natywny jak i zarządzany. Działa jedynie dla niezbyt zagłębionych crossreferencji. Otrzymujemy go w postaci wtyczki do Visual Studio.

Z ostatniej chwili:


## Orange Heap


[http://orangeheap.blogspot.com/](http://orangeheap.blogspot.com/)
Świeżynka, pierwsza, publiczna wersja wydana 7 września 2011. Wersja obecnie udostępniona czasem łapie zawias i po zrobieniu obfuskacji nie zapisuje nigdzie zmian. Jednakże widać, że projekt ma szanse na zaistnienie w śród darmowych obusfkatorów.

A jak by się komuś nudziło:


## Obfuscar


[http://code.google.com/p/obfuscar/](http://code.google.com/p/obfuscar/)
Program wywoływany z konsoli. Bez większych rewelacji.


## NetOrbiter


[http://www.zolohouse.com/wow/NetOrbiter/index.html](http://www.zolohouse.com/wow/NetOrbiter/index.html)
Aplikacja w wersji beta/demo, raczej jako ciekawostka.



## SharpObfuscator


[http://sharpobfuscator.codeplex.com/](http://sharpobfuscator.codeplex.com/)
Nierozwijana już od kilku lat. Kolejna ciekawostka w świecie obfuskacji .NET.


Gorąco polecam Eazfuscator.NET razem z Skater .NET LE. Ten pierwszy, mimo niesamowicie prostej obsługi, jest zaawansowanym obfuskatorem. Jeśli zaś czasem trzeba obfuskować jakieś pliki z zaawansowanymi corssreferencjami, warto skorzystać z Skater .NET LE.

Z zaciekawieniem będę również obserwował Orange Heap.

Aplikacje nie dają 100% pewności zatajenia kodu, ale dzięki nim, chociaż utrudnimy analizę po dekompilacji naszej aplikacji (np.świetnym NET Reflector'em).


 * Dziękuję i Pozdrawiam* 




