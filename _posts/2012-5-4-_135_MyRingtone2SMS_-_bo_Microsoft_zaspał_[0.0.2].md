---
layout:     post
title:      MyRingtone2SMS - bo Microsoft zaspał [0.0.2]
date:       2012-05-04 11:25:00
summary:    Temat ograniczeń Windows Phone był poruszany wiele razy. Brak przesyłania plików poprzez Bluetooth, brak slotu na pamięć SD itp. Dla mnie osobiście te braki nie przeszkadzają, gdyż nawet jakby te funkcjonalności były, pewnie bym ich nie używał :) Ale, jest jedno ale. W Windows Phone brakuje mi pewne...
categories: oprogramowanie programowanie urządzenia mobilne
---



Temat ograniczeń Windows Phone był poruszany wiele razy. Brak przesyłania plików poprzez Bluetooth, brak slotu na pamięć SD itp. Dla mnie osobiście te braki nie przeszkadzają, gdyż nawet jakby te funkcjonalności były, pewnie bym ich nie używał :) Ale, jest jedno ale. W Windows Phone brakuje mi pewne jednej, malutkiej funkcjonalności, maluteńkiej. Otóż nie można zmienić dzwonka SMS na swój własny! Tego nie mogę zrozumieć!

Postanowiłem zatem napisać własną aplikację do ustawiania dźwięków SMS, ale po kolei... :)



## Historia własnych dzwonków w Windows Phone



Może trochę historii. Pierwsze wydanie Windows Phone 7 nie pozwalało na ustawienie własnego dzwonka. Nigdzie. Byliśmy skazani na domyślne dzwonki, nie były one złe, ale... uwielbiam dzwonek SMS "Power Rangers" :D To była załóżmy epoka  *kamienia łupanego* . Czasy  *obecne*  nadeszły, wraz z premierą Windows Phone 7.5 Mango. I cóż otrzymaliśmy w raz z premierą nowej wersji systemu? Oczywiście wiele, bardzo dużo nowych rzeczy w tym... zmiana dzwonka nadchodzącego połączenia! Wreszcie!



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-4-_135_/g_-_288x192_-_-_31942x20120502114537_0.jpg)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-4-_135_/g_-_288x192_-_-_31942x20120502114629_0.jpg)



Mango udostępnił dla aplikacji możliwość zapisu dźwięków jako dzwonków. Dzięki czemu, pojawiają się one na liście w ustawieniach. Świetnie, wreszcie można ustawić własny dzwonek. Ok, tylko zaraz... nadal nie ma zmienić dzwonka SMS! Cóż, czas wziąć się do roboty! :P



## MyRingtone2SMS - ustaw własny dzwonek SMS!



Skoro Mango (zanosi się na to, że w Tango/Refresh również nie będziemiało tej opcji) nadal nie oferuje zmiany dzwonka SMS na własny, postanowiłem zmienić tą sytuacje :) A co! :P

[Dzięki SDK, które udostępnił Heathcliff74](http://www.wp7roottools.com/), możliwy jest dostęp bezpośrednio do plików na dysku i "grzebanie" w rejestrze. Cóż, kilka chwil na XDA Developers i okazuje się, że pliki dzwonków zapisywane są w folderze  *"\My Documents\My Ringtones\"* , zaś dzwonki SMS dla dostawców OEM w folderze  *Windows* . Jeszcze kilka zmian w rejestrze i dzwonek SMS pojawia się na liście dostępnych dzwonków do wiadomości tekstowych w opcjach systemu.

W taki sposób powstał pomysł  na aplikację MyRingtone2SMS. Program odczytuje dostępne dzwonki, jakie zostały pobrane poprzez aplikacje zewnętrzne np. [Free Ringtones](http://www.windowsphone.com/en-US/apps/46a064d2-1375-4052-94f6-80da09f76c86). Lista dzwonków widoczna jest na ekranie głównym. Wystarczy teraz zaznaczyć któraś pozycję, aby pokazała się ona na liście z wyborem dzwonka SMS (Ustawienia).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-4-_135_/g_-_288x192_-_-_31942x20120502120238_0.jpg)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-4-_135_/g_-_288x192_-_-_31942x20120502120247_0.jpg)





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-4-_135_/g_-_288x192_-_-_31942x20120502120448_0.jpg)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-4-_135_/g_-_288x192_-_-_31942x20120502120453_0.jpg)




Jako autor MyRingtone2SMS, używam jej już kilka dni i nie stwierdziłem żadnych skutków ubocznych :) Polecam do przetestowania i wyrażenia swojej opinii, uwag, sugestii itp. 
Z góry dziękuję :)



### MyRingtone2SMS - wymagania


Aplikacja wymaga praw roota, ze względu na użycie WP7 Root Tools SDK. Aby odpalić MyRingtone2SMS musisz mieć jedną z opcji:


  * zainstalowany custom rom

lub

  * zainstalowany [WP7 Root Tools](http://www.dobreprogramy.pl/djfoxer/Rootowanie-w-Windows-Phone-dla-wszystkich,31248.html), aby móc nadać uprawnienia roota dla aplikacji (instalacja WP7 Root Tools wymaga posiadania odblokowania interop)




### MyRingtone2SMS - change log



0.0.1 

  * pierwsza wersja


0.0.2 

  * dodanie pobierania dzwonków z folderu  *"\My Documents\Ringtones\"* 


  * wykrywanie niespójności danych, z możliwością uśnięcia danych z rejestru





### MyRingtone2SMS - download



 *[MyRingtone2SMS 0.0.1](http://www.djfoxer.pl/MyRingtone2SMS_0.0.1.xap)

[MyRingtone2SMS 0.0.2 ](http://www.djfoxer.pl/MyRingtone2SMS_0.0.2.xap)

* 


Krótki filmik z 1800pocketpc:


[youtube=http://www.youtube.com/watch?v=K-IDZoi-wdo]
