---
layout:     post
title:      DP PostTagger - wtyczka do Chrome tagująca wpisy na blogu dobrychprogramów
date:       2012-08-13 18:13:00
summary:    Oto jest, długo oczekiwana (czyż, nie?) wtyczka do Chrome, która taguje wpisy, oczekujące do wejścia na stronę główną.Czym jest DP PostTagger i jak działa?DP PostTagger to wtyczka do Chroma (mego autorstwa - djfoxer © 2012  — P ), która otagowuje (oznakowuje) wpisy na blogu. Jednakże, nie sprawdza ona każdy wpis, ale tylko te, które są w dziale oczekujących na wejście na stronę główną (zakładka "poz...
categories: oprogramowanie internet porady
slug: DP-PostTagger-wtyczka-do-Chrome-tagujaca-wpisy-na-blogu-dobrychprogramow,35520.html
---



Oto jest, długo oczekiwana (czyż, nie?) wtyczka do Chrome, która taguje wpisy, oczekujące do wejścia na stronę główną.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120809102149_0.png)




## Czym jest DP PostTagger i jak działa?


DP PostTagger to wtyczka do Chroma (mego autorstwa - djfoxer © 2012 :P ), która otagowuje (oznakowuje) wpisy na blogu. Jednakże, nie sprawdza ona każdy wpis, ale tylko te, które są w dziale oczekujących na wejście na stronę główną (zakładka "pozostałe"). 

W tym dziale pojawiają się wpisy, które jeszcze nie zdążyły być przeanalizowane przez Redakcję lub te, które nie nadawały się na główną. Nazwać to można "wylęgarnią", czy "wykopaliskiem". Zatem są tam przyszłe teksty, które znajdziemy w wyróżnionych i takie, które nic nie wnoszą, a jedynie marnują czas Czytelników.

Otóż dla Was, czyli dla Czytelników bloga dobrychprogramów, powstała wtyczka DP PostTagger! Jej głównym zadaniem jest otagowanie wpisów w zakładce "pozostałe", które mogę być potencjalnym traceniem czasu. Do oznakowania wpisów posłużyłem się kilkoma parametrami, które są w pełni konfigurowane z poziomu opcji wtyczki.

Wtyczka dla każdego wpisu w zakładce "pozostałe" dodaje tagi, które omówione zostaną w następnym punkcie.  Wystrczy kliknąć na link "pozostałe", by DP PostTagger rozpoczął działanie. Każdy wpis jest analizowany oddzielnie i asynchronicznie.  Analiza trwa w tle, nie zakłócając normalnej pracy. Jeśli jakiś warunek jest spełniony dla danego wpisu, otrzymuje on oznakowanie.

Wtyczka DP PostTagger posiada moduł auto-aktualizacyjny!


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813165800_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813165828_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813180645_0.png)





## Sposób tagowania

Sposób tagowania obejmuje kilka, konfigurowalnych w ustawieniach DP PostTaggera, parametrów. Ich wybór był propozycją Waszą, czyli blogerów na portalu. Nie będę uzasadniał wyboru konkretnych parametrów, które tagują wpisy, ale przejdę do omawiania jakie metody zostały zaimplementowane. Wyjaśnienie wyboru tych, a nie innych współczynników tagowania nie ma sensu, gdyż są raczej logiczne.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813165733_0.png)



### Liczba dni po rejestracji

Pierwszym oznaczeniem jest liczba dni, jaka upłynęła od rejestracji. Jeśli liczba jest mniejsza niż ustawiona w opcjach (domyślnie 60), wówczas pojawi się zielone pole z informacją, ile upłynęło czasu od powstania konta. 


### Liczba wpisów

Tag (kolor żółty) z ilością wpisów na blogu, który pojawia się, jeśli liczba wpisów jest poniżej zadanej w ustawieniach wtyczki (domyślnie - 6).


### Liczba komentarzy

Kolejne oznaczenie to ilość komentarzy dodanych na portalu przez autora wpisu. Jeśli liczba jest mniejsza niż ustawiona w opcjach (domyślnie 30), wówczas pojawi się niebieskie pole z informacją, ile autor dodał komentarzy na portalu.


### Liczba znaków we wpisie

W opcjach można ustawić minimalną liczbę akceptowalnych znaków, jakie powinien zawierać wpis. Jeśli ilość znaków nie przekracza ustalonej liczby (domyślnie 1200), wówczas pojawi się pomarańczowy znacznik "Uwaga na wpis!".


### "Zakazane" słowa w tytule wpisów

Ostatnią opcją jest możliwość dodania słów w tytule wpisu, które będą uznawane za "niebezpieczne". Mogą być to również części słów. Domyślnie są to słowa "wita" (ze względu n to, iż takie słowo klucz, będzie pasowało do słów: witam, witajcie) i "cześć". Można rozszerzyć słownik o inne słowa poprzez opcje wtyczki. Jeśli słowo klucz zostanie wyłapane w tytule, wpis zostaje otagowany pomarańczowym znacznikiem "Uwaga na wpis!". 


## Opcje


Wszystkie wymienione powyżej metody tagowania można łatwo dostosować do swoich potrzeb w ustawieniach wtyczki.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813170124_0.png)



Po zmianach należy zapisać nowe ustawienia poprzez wciśnięcie przycisku "Zapisz opcje".


## Instalacja

Z racji tego, iż nie posiadam (jeszcze? :P ) konta w Chrome Web Store, nie można zainstalować jej poprzez sklep Google Chroma. Nie ma jednak co rozpłaczać, gdyż instalacja jest dziecinnie prosta i zajmie kilka sekund. Oto co należy zrobić:




  * otwieramy okno z rozszerzeniami: "kluczyk" -> "Narzędzia" -> "Rozszerzenia"  lub wpisujemy w nowym oknie: chrome://chrome/extensions/


  * wchodzimy na stronę z wtyczką [http://www.djfoxer.pl/DPPostTagger/DPPostTagger.crx](http://www.djfoxer.pl/DPPostTagger/DPPostTagger.crx)


  * pojawi się ostrzeżenie, iż wtyczka jest spoza Chrome Web Store, klikamy OK


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813173600_0.png)


  * pomimo tego, wtyczka zapisała się na dysku, odnajdujemy ją (np. poprzez "Pokaż w folderze")


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813173921_0.png)


  * wystarczy teraz przeciągnąć plik DPPostTagger do otwartego okna "Rozszerzenia" w Chrome, aby ją zainstalować


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813174149_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-8-13-_125_/g_-_608x405_-_-_35520x20120813174429_0.png)



Od tej pory wtyczka będzie aktywna na stronie [http://www.dobreprogramy.pl/Blog.html](http://www.dobreprogramy.pl/Blog.html), po przejściu na zakładkę "pozostałe".


## Podsumowanie


Mam nadzieję, że wtyczka będzie z chęcią przez Was używana. Liczę na odzew z waszej strony odnośnie DP PostTaggera. Mile widziane będą opinie i sugestie. Przyjemnego czytania blogów na dobrychprogramach:)