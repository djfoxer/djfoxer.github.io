---
layout:     post
title:      Aktualizacja Punk Bustera (ręczna)
date:       2010-10-24 12:42:00
summary:    WstępWitam, kilka osób było zainteresowanych sposobem ręcznej aktualizacja Punk Bustera. Temat jest dość ważny dla graczy (w moim przypadku CoD4), gdyż często z "niewiadomych" przyczyn Punk Buster dostarczony z grą ,w wielu przypadkach nie jest w stanie zaktualizować się do najnowszej wersji.Jest to bezpośredni powód powstawania lagów w grze lub/oraz niemożności podłączenia się do serwerów wymagaj...
categories: oprogramowanie porady gry
slug: Aktualizacja-Punk-Bustera-reczna,21147.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-10-24-_211_/g_-_-x-_-_-_x20101024120951_2.png
---





## Wstęp




Witam, kilka osób było zainteresowanych sposobem ręcznej aktualizacja Punk Bustera. 
Temat jest dość ważny dla graczy (w moim przypadku CoD4), gdyż często z "niewiadomych" przyczyn Punk Buster dostarczony z grą ,w wielu przypadkach nie jest w stanie zaktualizować się do najnowszej wersji.

Jest to bezpośredni powód powstawania lagów w grze lub/oraz niemożności podłączenia się do serwerów wymagających nowszej wersji Punk Bustera, gdyż aktualizacja Punk Bustera próbuje cały czas ściągnąć nowszą wersję. 

Małe śledztwo doprowadziło do odkrycie ciekawej zależności. Otóż problemem może być to, iż starsza wersja Punk Bustera "nie pozwala" się odinstalować. Gdyż zarówno PnkBstrA i PnkBstrB są usługami systemu Windows.





## Rozwinięcie




Problem ten można rozwiązać dość szybko i bezboleśnie.

1. 
Usuwamy (jeśli istnieje) katalog z Punk Busterem w folderze z grą.

2. 
Uruchamiamy narzędzie zarządzania usługami i zatrzymujemy następujące usługi:

[code]PnkBstrA
PnkBstrB
[/code]




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-10-24-_211_/g_-_-x-_-_-_x20101024120951_2.png)



3. 
Używając opcji do wyszukiwania pików (także ukrytych) da folderu WINDOWS wpisujemy frazę:

[code]pnkbstr[/code]


W moim przypadku znaleziono następujące pliki:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-10-24-_211_/g_-_-x-_-_-_x20101024114939_1.png)



Spokojnie możemy usunąć wszystkie wyszukane pliki i uruchamiamy ponownie komputer.
UWAGA!Jeśli pliki nie będą dały się usunąć, w kroku 2. należy dodatkowo we właściwościach dla usługi wybrać  typ uruchomienia: Wyłączony i przed zastosowaniem kroku 3., uruchomić ponownie komputer.

4. 

Z oficjalnej strony Punk Bustera ściągamy program PBSetup, do automatycznej aktualizacji:
[http://websec.evenbalance.com/downloader/download.php?file=1](http://websec.evenbalance.com/downloader/download.php?file=1) 

5. 

Uruchamiamy ściągnięty program i dodajemy grę dla jakiej chcemy zaktualizować/zainstalować Punk Bustera:
- klikamy "Add Game" (A)
- z listy rozwijanej, w nowo otwartym oknie, wybieramy grę (B) 
- klikamy na "Add Game" (C) 
- klikamy na "Check for Updates" (D) 
PBSetup powinien sam ściągnąć nową wersje Punk Bustera i aktualizacje



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-10-24-_211_/g_-_-x-_-_-_x20101026174822_3.png)



Możemy cieszyć się nowym Punk Busterem i grą :)





## Zakończenie




Mam nadzieję, iż komuś ten tekst pomógł w walce z Punk Busterem. Proszę o opinie, komentarze i propozycje. Dzięki za czytanie :)

