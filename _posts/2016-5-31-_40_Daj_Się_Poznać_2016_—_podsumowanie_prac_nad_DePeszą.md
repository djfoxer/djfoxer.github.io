---
layout:     post
title:      Daj Się Poznać 2016 — podsumowanie prac nad DePeszą
date:       2016-05-31 16:59:00
summary:    Konkurs Daj Się Poznać 2016, organizowany przez Macieja Aniserowicza, można już uznać za zakończony. Jego celem było promowanie ciekawych pomysłów, blogów i ludzi związanych z programowaniem. O szczegóły odsyłam do pierwszego wpisu z marca. W ramach konkursu, w którym udział wzięło niemalże 300 osób...
categories: <input id="chkTagsList_3" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_3" checked="checked" value="8"><label for="chkTagsList_3">oprogramowanie</label> <input id="chkTagsList_7" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_7" checked="checked" value="128"><label for="chkTagsList_7">programowanie</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



Konkurs [Daj Się Poznać 2016](http://devstyle.pl/daj-sie-poznac/), organizowany przez [Macieja Aniserowicza](http://devstyle.pl/o-mnie/), można już uznać za zakończony. Jego celem było promowanie ciekawych pomysłów, blogów i ludzi związanych z programowaniem. O szczegóły odsyłam do pierwszego [wpisu z marca](http://www.dobreprogramy.pl/djfoxer/Powiadomienia-z-dobreprogramy.pl-na-Windows-konkurs-Daj-sie-poznac-2016,71094.html). 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530182959_0.png)



W ramach konkursu, w którym udział wzięło  *niemalże 300 osób*  (!!!), postanowiłem stworzyć aplikację dla użytkowników portalu dobreprogramy.pl. Już od jakiegoś czasu krążył po mojej głowie pomysł, aby przenieść system powiadomień ze strony www do aplikacji, która w tle sama sprawdzałaby nowe notyfikacje. Była ona adresowana do  *wąskiej*  grupy odbiorców, czyli do najbardziej aktywnych użytkowników portalu (oczywiście zwrot  *wąska*  grupa proszę nie brać dosłownie :P ). Od początku wiedziałem, co chce osiągnąć, dzięki czemu finalny stan na koniec akcji blogowej jest bardzo satysfakcjonujący. 

Z racji tego, iż na co dzień związanych jestem z rozwiązaniami Microsoftowymi (.NET, MS SQL), postanowiłem projekt aplikacji stworzyć w C#, a dokładniej w oparciu o nową platformę Universal Windows Platform. Było to dla mnie czymś nowym i stanowiło swego rodzaju wyzwanie, możliwość rozwoju, ale także stworzenie czegoś, co będzie przydatne współużytkownikom portalu dobreprogramy.pl, z którym wszyscy tu jesteśmy związani.  

Spis wszystkich wpisów z serii można znaleźć pod tym linkiem:
<blockquote>
<p>Seria wpisów: [Aplikacja Windows 10 (Mobile) do powiadomień z dobreprogramy.pl](http://www.dobreprogramy.pl/djfoxer/Aplikacja-Windows-Mobile-do-powiadomien-z-portalu-dobreprogramypl,s229.html)</p>
</blockquote>



## Podsumowanie prac



Całościowo projekt po tych trzech miesiącach wypada niezmiernie pozytywie. Tak naprawdę udało się osiągnąć znacznie więcej niż zakładałem. Cieszę się, że stworzona seria składa się w wpisów, gdzie każdy z nich jest niezmiernie obszerny i wartościowy. Przyznaję, że wymagało to sporo pracy i poświęceń, ale było warto :) Postanowiłem w kilku punktach zawrzeć najważniejsze informacje o projekcie.



  * Powstała w pełni funkcjonalna,  aplikacja na Windows 10 i Windows 10 Mobile do obsługi powiadomień z portalu dobreprogramy.pl, która dostępna jest już w wersji finalnej w markecie: [DePesza](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2)


  * Aplikacja nie tylko działa, ale równie całkiem nieźle wygląda i doczekała się własnego logo



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530192214_0.jpg)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530192218_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530192217_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530192217_1.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530192359_0.png)






  * Stworzona została dodatkowa funkcjonalność - pobieranie globalnych, statystyk z bloga (znaczne ułatwienie dla blogerów)


  * Powstała niezmiernie szczegółowa analiza systemu logowania i zarządzania powiadomieniami na portalu dobreprogramy.pl  (swego rodzaju reverse engineering)


  * Powstał ciekawy zestaw wpisów odnośnie tworzenia aplikacji w Universal Windows Platform


  * Napisałem nawet testy jednostkowe (:P), która finalnie okazały się niezbędne nawet przy tak niewielkim projekcie



  * Sumarycznie (na dzień tworzenia tego wpisu): 
 *ponad 52 000*  wyświetleń, 3 *40 komentarzy* 


  * Najbardziej poczytny wpis: [Wyskakujące powiadomienia w Windows 10](http://www.dobreprogramy.pl/djfoxer/Wyskakujace-powiadomienia-w-Windows-10-aplikacja-portalowa-w-UWP,71904.html) ( *10 000*  wyświetleń)



  * Sporym sukcesem było również ogłoszenie konkursu na nazwę aplikacji, dzięki czemu program z bezdusznego okienka w komputerze/smartfonie stał się poczciwą  *DePeszą* 



  * Udostępniona kilka dni temu finalna wersja aplikacji ma ponad 200 unikalnych użytkowników i średnią ocenę w markecie 4.4


  * Zaangażowanie społeczności portalowej w rozwój aplikacji (duży odzew w konkursie na nazwę, zgłaszane błędy i nowe pomysły) 


  * Pierwsza seria wpisów o analizie, wyróżniona w comiesięcznym konkursie blogowym na portalu dobreprogramy.pl


  * Pełen kod źródłowy dostępny na GitHub: [https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification) 







<blockquote>
<p>Sumarycznie (na dzień tworzenia tego wpisu): 
 *ponad 52 000*  wyświetleń, 3 *40 komentarzy* , najbardziej poczytny wpis: [Wyskakujące powiadomienia w Windows 10](http://www.dobreprogramy.pl/djfoxer/Wyskakujace-powiadomienia-w-Windows-10-aplikacja-portalowa-w-UWP,71904.html) ( *10 000*  wyświetleń)</p>
</blockquote>

<blockquote>
<p>Powstała szczegółowa analiza systemu logowania i zarządzania powiadomieniami na portalu dobreprogramy.pl, seria wisów o tematyce Universal Windows Platform, jak i czystym C#</p>
</blockquote>

<blockquote>
<p>Wsparcie czytelników - konkurs na nazwę, logo DePeszy, zgłaszanie błędów i nowych pomysłów</p>
</blockquote> 

<blockquote>
<p>Powstała aplikacja, która od kilku dni jest już w wersji finalnej w markecie Windows:  [DePesza](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2)</p>
</blockquote>



## Co dalej?


Aplikacja na Windows 10 i Windows 10 Mobile można uznać za produkt skończony. Zapewne będą jeszcze wrzucane pomniejsze poprawki związane z UI lub wyłapanymi błędami. W tym momencie głównie skupię się już jednak na stworzeniu aplikacji na pozostałe platformy przy użyciu Xamarina.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530194609_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_40_/g_-_608x405_-_-_73595x20160530194609_1.png)





## Słowo na koniec

 

Przyznaję, że ciekawy projekt, który pierwotnie miał być aplikacją do własnego użytku, stał się DePeszą - programem dla czytelników portalu dobreprogramy.pl.

Dziękuję tutaj wszystkim osobom, które zgłaszały błędy, nowe propozycje, brały udział w konkursie na nazwę i comiesięczny konkurs blogowy. Mam nadzieję, że DePesza, tym razem już multiplatformowa, ujrzy światło dzienne równie szybko, jak omawiana wersja na platformę UWP.


