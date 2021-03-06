---
layout:     post
title:      Migracja starej wtyczki do nowej wersji Visual Studio 2017
date:       2017-05-17 20:17:00
summary:    Tworząc dodatek do Visual Studio zapewne wiele osób będzie uczyło się poprzez analizę kodu istniejących już dodatków (chociażby ze źródeł na GitHubie od MS ). Okazuje się jednak, że projekty pluginów stworzonych pod stare IDE zupełnie nie chcą kompilować się w nowej odsłonie Visual Studio. Jesteśmy zmuszeni do ręcznej migracji takich dodatków. Oto poradnik jak tego dokonać.Automatyczna aktualizacj...
categories: oprogramowanie porady programowanie
slug: Migracja-starej-wtyczki-do-nowej-wersji-Visual-Studio-2017,81088.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193841_0.png
---



Tworząc dodatek do Visual Studio zapewne wiele osób będzie uczyło się poprzez analizę kodu istniejących już dodatków (chociażby [ze źródeł na GitHubie od MS](https://github.com/Microsoft/VSSDK-Extensibility-Samples) ). Okazuje się jednak, że projekty pluginów stworzonych pod stare IDE zupełnie nie chcą kompilować się w nowej odsłonie Visual Studio. Jesteśmy zmuszeni do ręcznej migracji takich dodatków. Oto poradnik jak tego dokonać.



## Automatyczna aktualizacji (standardowa)



Otwierając projekt, który został stworzony w starym IDE, w nowym Visual Studio 2017 dostaniemy standardowy komunikat o automatycznej aktualizacji.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193841_0.png)



Nie mamy wyjścia i godzimy się na to. Po chwili projekt jest już gotowy na działanie w nowej wersji IDE. Niestety próba builda zakończy się niepowodzeniem. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193842_0.png)



W tym momencie musimy sami przejść przez kluczowe elementy projektu, aby zaktualizować ręcznie dodatek.



## Nowe paczki z NuGeta



Zaczniemy migrację o pobrania nowych paczek z NuGeta. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193842_1.png)



Na zakładce aktualizujemy dostępne nowe składniki i restartujemy IDE, jeśli jest to wymagane.



## Aktualizacja vsixmanifest


Kolejnym krokiem jest przejrzenie pliku  *source.extension.vsixmanifest*  z definicjami wymagań co do wtyczki i docelowej wersji Visual Studio. Zaczniemy od zakładki  *Install Targets* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193842_2.png)



W starej wersji widzimy, iż wtyczka ustawiona była na zgodność jedynie z VS 2015. Rozszerzmy zatem kompatybilność na kolejne wersje. Musimy użyć tutaj zakresu, który określa jakie numery wersji będą wspierane. Można podać konkretne numery np. [14.0,15.0], ale w tym przypadku ustawimy zakres otwarty, bez wpisywania górnej granicy: [14.0,). Dodatkowo dodamy kompatybilność dla edycji Community i Enterprise:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193842_3.png)



W następnej kolejności zaktualizujemy zależność na zakładce  *Dependecies* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517193842_4.png)



Tu również pozostawimy możliwość instalacji dla przyszłych wersji IDE:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200251_0.png)



Ostatnia zakładka jest bardzo ważna, gdyż pojawiła się ona dopiero w Visual Studio 2017. Określa ona elementy jakie muszą być zainstalowane, aby nasza wtyczka mogła działać. W tym przypadku dodałem zależność, która określa istnienie edytora IDE co najmniej w wersji 14.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200252_0.png)



Po tych czynnościach będziemy już w stanie zbuildować dodatek. 




## Debugowanie


Pomimo tego iż projekt już się buduje, nie będziemy w stanie go debugowac (w przypadku, gdy nie mamy starej wersji Visual Studio).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200252_1.png)



Problemem jest debuger, który uruchamia sklonowaną instancję Visual Studio. W tym przypadku chce on uruchomić starszą edycję IDE. Zatem ostatnim krokiem zastaje już tylko podmiana ścieżki na nową:

 

> C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\devenv.exe


Dokonamy tego we właściwościach projektu, na zakładce  *Debug* , zaznaczając pole  *Start external program*  i podając ścieżkę do nowego IDE (przykład wyżej).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200252_2.png)



Po tych krokach projekt zbuilduję się i będzie możliwe debugowanie go w nowym oknie IDE:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200252_3.png)





Przypominam, że dostępna jest już w markecie Visual Studio wczesna wersja wtyczki konkursowej Healthy With VS.



> Dodatek dostępny jest w markecie pod adresem: [Healthy With VS](https://marketplace.visualstudio.com/items?itemName=djfoxer.HealthyWithVS)
.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200751_0.PNG)




Zachęcam do pobierania i testowania pierwszej wersji. Liczę również na feedback z waszej strony.



> Źródła dostępne są na GitHubie (branch master i POC):
> [https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-17-_22_/g_-_-x-_-_-_x20170517200803_0.png)

