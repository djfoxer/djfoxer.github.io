---
layout:     post
title:      Konkurs na nazwę aplikacji dobreprogramy.pl, a także niesforny Visual Studio
date:       2016-04-11 21:47:00
summary:    Tworząc uniwersalną aplikację do powiadomień z portalu dobreprogramy natknąłem się na bardzo ciekawy problem.  Postanowiłem opisać ową przygody, a także zapytać Was o pomysł na nazwę aplikacji portalowej :)Na początku skupmy się jednak na ciekawym przypadku...Device cannot be foundW ostatnim czasie ...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_7" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_7" checked="checked" value="128"><label for="chkTagsList_7">programowanie</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



[Tworząc](http://www.dobreprogramy.pl/djfoxer/Wyskakujace-powiadomienia-w-Windows-10-aplikacja-portalowa-w-UWP,71904.html) uniwersalną aplikację do powiadomień z portalu dobreprogramy natknąłem się na bardzo ciekawy problem.  Postanowiłem opisać ową  *przygody* , a także zapytać Was o pomysł na nazwę aplikacji portalowej :)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411213104_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214636_0.jpg)


Na początku skupmy się jednak na ciekawym przypadku...




## Device cannot be found


W ostatnim czasie dostaliśmy najnowszą aktualizację Update 2 do Visual Studio 2015. Oczywiście wersja Community, którą używam, otrzymała również ową paczkę. Okazało się jednak, że po tej aktualizacji VS przy próbie wrzucenia aplikacji portalowej na smartfon zaczął rzucać błędem:

<blockquote>
<p>Bootstrapping failed. Device cannot be found. 0x89731810: Deployment failed because no Windows Phone was detected. Make sure a phone is connected and powered on.</p>
</blockquote>

Żeby jeszcze bardziej zaciemnić obraz, w tym samym czasie wgrałem (ponownie!) na Lumię 925 Windows 10 Mobile z gałęzi Redstone. 

Stanąłem przed niebłahym problemem. Visual Studio przestał wykrywać mój telefon. Pierwsze podejrzenia padły na Redstone. Tutaj po pewnym czasie spędzonym z Google stwierdziłem, że owa aktualizacja nie mogła jednak zepsuć detekcji urządzenia. Próbowałem jednak resetować tryb deweloperski w smartfonie i kombinować z konfiguracją urządzenia. Nadal bezskutecznie.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411210204_0.PNG)



Kolejne podejrzenie padło na VS. Cóż, po kilkudziesięciu chwilach w Google zdecydowałem się na przeinstalowanie IDE. Miałem nadzieje, że ostatecznie rozwiążę to moje problemy. 

Niestety nic to nie zmieniło. Natknąłem się jednak na link, który pomógł mi dwa lata temu z problem przy prawidłowym działaniu [Project My Screen](http://www.dobreprogramy.pl/djfoxer/Project-My-Screen-udostepnianie-ekranu-Windows-Phone-8.1-na-ekran-komputera-po-kablu-USB,53799.html), Okazało się, że należy usunąć sterowniki związane ze smartfonem z systemu (!!!), poprzez Menadżer urządzeń:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411210204_1.png)



Zapewne podczas aktualizacji Update 2 do VS, pakiet instalacyjny dodał nowe sterowniki do urządzeń przenośnych, ale nie był w stanie podmieć tych, który były związane już z zainstalowanymi urządzeniami. Uwierzcie, że problem nie jest trywialny do zdiagnozowania, gdyż w sieci jest bardzo dużo wątków, które nie podają faktycznego rozwiązania.

Przejdźmy jednak do sedna...




## Konkurs na nazwę aplikacji portalowej





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411215252_0.jpg)



Tworząc aplikację natknąłem się na jeszcze jeden ciekawy  *"problem"* :

<blockquote>
<p>Jak ma nazywać się aplikacja od obsługi powiadomień z portalu dobreprogramy.pl? :)</p>
</blockquote>



Proszę Was zatem o pomoc. W komentarzach piszczcie jak wg Was powinna nazywać się aplikacja portalowa. Niczego nie sugeruję, ale aby pomóc Wam postanowiłem nagrodzić najlepsze propozycje. Wybór będzie subiektywny, a TOP 5 najlepszych nazw nagrodzę kodami do gier na Steam:



### Murdered: Soul Suspect




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214358_3.jpg)




### The Last Remnant




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214358_4.jpg)




### Overlord + Overlord Raising Hell (Expansion)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214358_0.jpg)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214358_1.jpg)




### Life Is Strange - Episode 1




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214534_0.jpg)




### Hospital Tycoon




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411214358_2.jpg)



 
Rozwiązanie konkursu w następnym tygodniu. Liczę na Waszą pomoc :)

Nagrody ufundowałem sam :) W zależności od zainteresowania może coś jeszcze dorzucę ;) :P 



Sama aplikacja już nabiera kształtów ;) Zapewne jeszcze w tym tygodniu pojawi się wpis, odnośnie sposobu działania aplikacji w tle i zapamiętywania danych. Przedstawię również ograniczenia, jakie naniósł MS na UWP  (Universal Windows Platform).











<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-11-_47_/g_-_608x405_-_-_72207x20160411210205_0.png)

