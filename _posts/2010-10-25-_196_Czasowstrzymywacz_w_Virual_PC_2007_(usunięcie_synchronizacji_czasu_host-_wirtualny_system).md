---
layout:     post
title:      Czasowstrzymywacz w Virual PC 2007 (usunięcie synchronizacji czasu host->wirtualny system)
date:       2010-10-25 19:33:00
summary:    Na początekWitajcie. Często korzystając z wirtualki zauważamy, iż maszyna wirtualna jest synchronizowana z czasem hosta (gospodarza, czyli z naszym realnym systemem). Nie zawsze jest to nam na rękę (np. testy oprogramowania itp.). Zmiana testowana była na Virtual PC 2007 SP1, który można zainstalowa...
categories: windows oprogramowanie porady
---





## Na początek



Witajcie. 
Często korzystając z wirtualki zauważamy, iż maszyna wirtualna jest synchronizowana z czasem hosta (gospodarza, czyli z naszym realnym systemem). Nie zawsze jest to nam na rękę (np. testy oprogramowania itp.). Zmiana testowana była na Virtual PC 2007 SP1, który można zainstalować na Windows: XP, VISTA, 7. Do dzieła!





## Działamy




1. 
Zatrzymaj (jeśli jest uruchomiona) maszynę wirtualna, dla której chcesz wprowadzić zmiany.

2. 
Zlokalizuj plik .VMC dla danej maszyny wirtualnej (może to być np. folder w Dokumentach: (...)\My Virtual Machines\[moja_nazwa]\[moja_nazwa].vmc)

3. 
Edytuj np. Notatnikiem i znajdź blok:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-10-25-_196_/g_-_608x405_-_-_21163x20101025191440_1.png)

 

i pod tym blokiem dopisujemy własny blok:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-10-25-_196_/g_-_608x405_-_-_21163x20101025191440_2.png)

 

Link z kodem do przyklejenia:

[http://paste-it.net/public/rc94a4a/xml/](http://paste-it.net/public/rc94a4a/xml/)


(do Redakcji/Czytających to: jak zrobić aby znaczniki html/xml wyświetlały się poprawnie?, dla < &lt; czy &#60; nie działają!) 



## 4.



Zapisujemy plik .VMC i uruchamiamy maszynę wirtualną!
Gotowe! :)





## Koniec



Od tej pory czas maszyny wirtualnej nie będzie aktualizowany z czasem hosta. Podobno trik ten nie działa na Windows Virtual PC (wersja specjalna dla Windows 7), jednakże możliwość instalacji Virtual PC 2007 na Win 7 rozwiązuje bezboleśnie tą niedogodność.

Pozdrawiam.

