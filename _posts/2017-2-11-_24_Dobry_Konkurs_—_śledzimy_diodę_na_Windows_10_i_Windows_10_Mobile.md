---
layout:     post
title:      Dobry Konkurs — śledzimy diodę na Windows 10 i Windows 10 Mobile
date:       2017-02-11 11:26:00
summary:    Od kilku dni trwa konkurs z diodą na dobrychprogramach. Ponownie śledzić będziemy pojawienie się lampki LED w dzień i w nocy. Obserwować diodę można klasycznie, przez stronę www, a także z poziomu aplikacji na Androida i iOS. Co jednak z użytkownikami Windows?Dioda nie dla  wszystkich?Dioda 2017 w o...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_3" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_3" checked="checked" value="8"><label for="chkTagsList_3">oprogramowanie</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



Od kilku dni trwa [konkurs z diodą](https://konkurs.dobreprogramy.pl/) na dobrychprogramach. Ponownie śledzić będziemy pojawienie się  *lampki LED*  w dzień i w nocy. Obserwować diodę można klasycznie, przez stronę www, a także z poziomu aplikacji na Androida i iOS. Co jednak z użytkownikami Windows?



## Dioda nie dla  wszystkich?



Dioda 2017 w obecnej wersji jest zdecydowanie nastawiona na głosowanie przez aplikacje mobilne. Pomimo, że udzielenie odpowiedzi przez www jest zalecane przez Redakcję, to obecnie nie pozwala ono na szybkie wysłanie odpowiedzi na pytanie. Wiele osób skarży się na męczącą captche od Google, która zmusza do klikania po obrazkach. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210204057_0.PNG)



Minusem jest również to, że strona konkursowa jest zupełnie nieprzystosowana do głosowania przez urządzenia przenośne. Dodatkowo śledzenie diody przez www wymaga odświeżania strony.




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210204054_0.png)





Z tych też powodów dużo łatwiej jest obserwować diodę i udzielać odpowiedzi przez dedykowane aplikacje mobilne. Szkoda tylko, że Redakcja zadbała jedynie o użytkowników Androida i iOS. 



## Dobry Konkurs - aplikacja do konkursu z diodą  dla Windowsa



Postanowiłem jednak pomóc uciśnionym użytkownikom mobilnego Windowsa :P, a także ułatwić głosowanie przez desktopwego Windowsa. Poprzez analizę ruchu aplikacji mobilnej stworzyłem wersję aplikacji do głosowania w konkursie z diodą na multiplatformę UWP.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210212035_0.PNG)




Dostępna jest ona pod tym adresem w markecie Windows:

<blockquote>
<p>Dobry Konkurs - nieoficjalna aplikacja w konkursie Dioda na portalu dobreprogramy.pl na Windows 10 i Windows 10 Mobile - [link do marketu](https://www.microsoft.com/pl-pl/store/p/dobry-konkurs/9p2wmr76d2gm#) </p>
</blockquote>

<blockquote>
<p>Aplikacja umożliwiająca:
- logowanie/wylogowanie
- monitoring pytań w aplikacji
- pobranie pytania i odpowiedź na nie
- obsługa pytań otwartych, zamkniętych (jeden wybór) i z przesłaniem zdjęcia
- wyświetlenie i akceptacja regulaminu z uzupełnieniem danych</p>
</blockquote>

 Zatem użytkownicy mobilnego Windowsa 10 Mobile i desktopowego Windowsa 10 mogą głosować w konkursie znacznie szybciej i wygodniej. Dodatkowo aplikacja sama monitoruje diodę i informuje o jej pojawieniu się.



### Windows 10 Mobile





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210205017_0.png)





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210205023_0.png)



Aplikacja pozwala na udzielenie odpowiedzi na pytanie. Obsługuje on trzy typy odpowiedzi:


  * wybór jednej odpowiedzi z czterech (A, B, C, D)


  * udzielenie odpowiedzi na pytanie otwarte


  * udzielenie odpowiedzi na pytanie wymagające przesłania grafiki na serwer (z aparatu lub z lokalnej pamięci)







![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210205024_0.png)



Aplikacja potrafi monitorować diodę na bieżąco. W tym celu co 10 sekund następuje odpytanie serwera o pojawienie się pytania (15 min. jeśli zablokujemy ekran). Jeśli nie zablokujemy ręcznie ekranu w telefonie, to aplikacja sama zadba o to, aby ekran samoistnie się nie zablokował. Dotyczy oczywiście to tylko aplikacji na telefonie, na desktopie nie ma tego problemu. 

W przypadku, gdy pojawi się dioda, aplikacja poinformuje o tym poprzez wyświetlenie pytania i zapętlone odtwarzanie dźwięku syreny z łodzi podwodnej :) Nie sposób przegapić tego sygnału, idealne rozwiązanie do zostawienia na noc, aby aplikacja czuwała w trakcie nocy, aby wykryć diodę i nas obudzić.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210205024_1.png)





### Windows 10 desktop



UWP pozwala także na uruchomieni tej samej aplikacji na  *dużym*  Windows 10. Dzięki temu osoby z desktopową wersją okienek mogą jeszcze szybciej głosować w konkursie i śledzić diodę bez żmudnego odświeżania strony i patrzenia w ekran monitora.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210204049_0.PNG)





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-2-11-_24_/g_-_608x405_-_-_79130x20170210204050_0.PNG)





## Na koniec - ważne, kilka informacji do czytających


Aplikacja powstała moim nakładem pracy w wolnych chwilach.

<blockquote>
<p>Aplikacja Dobry Konkurs nie ma ona nic wspólnego z aplikacjami udostępnionymi przez Redakcję, aczkolwiek korzysta z tego samego API i jest to nieoficjalny  *port*  namaszczony przez Redakcję.</p>
</blockquote> 

<blockquote>
<p>Redakcja wyraziła także zgodę na to, aby umieścić ją w markecie i udostępnić dla wszystkich użytkowników.</p>
</blockquote>

Aplikacja Dobry Konkurs posiada wszystkie funkcje, które służą do monitorowania stanu diody i udzielenie odpowiedzi na pytanie. Nie ma tutaj listy rankingowej czy innych bajerów, które są zbędne przy udziale w konkursie.

Ogólnie na przyszłość poradziłbym redakcji pisanie takich apek w Xamarinie: szybko, multiplatformowo, z niezłymi efektami i w .NET. To ostanie o tyle jest ważne, że część Redakcji mogłaby w projekcie uczestniczyć jako deweloperzy. 

<blockquote>
<p>Aplikacja powstała kosztem zerwanych kilku nocek i poświęconego wolnego, prywatnego, czasu stąd też proszę nie marudzić, że coś brzydko wygląda lub nie jest do końca doszlifowane :) Robiłem to całkowicie bezinteresownie i bez niczyjego wsparcia :)</p>
</blockquote>

Aplikacja jest darmowa, ale jak ktoś chce to niech uznaje, że jest ona na licencji [beerware](https://pl.wikipedia.org/wiki/Beerware), więc jak coś, ktoś to proszę o prv :P 

<blockquote>
<p>W tej edycji nie mogę już obserwować diody tak, jak we wcześniejszych latach, stąd też udostępniłem swoją ciężką pracę dla was. Niech dobrze służy! :)</p>
</blockquote>

To chyba tyle, powodzenia! Czekam na feedback od was. 


