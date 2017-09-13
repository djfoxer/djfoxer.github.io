---
layout:     post
title:      Dysk SSD z Windows - konfiguracja
date:       2011-11-10 20:37:00
summary:    Wpis chcę zacząć od złożenia podziękowań na ręce Redakcji dobrychprogramów za wyróżnienie "bloger kwartału" i nagrodzenie dyskiem SSD (Kingston SSDNow V+100 96 GB - miodzio). Bardzo dziękuję za docenienie takiego szaraczka jak ja :) Mam nadzieję, że będę miał szansę się wyróżnić (i zasłużyć na wyróż...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_2" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_2" checked="checked" value="4"><label for="chkTagsList_2">sprzęt</label> <input id="chkTagsList_6" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_6" checked="checked" value="64"><label for="chkTagsList_6">porady</label>
---



 *Wpis chcę zacząć od złożenia podziękowań na ręce Redakcji dobrychprogramów za wyróżnienie "bloger kwartału" i nagrodzenie dyskiem SSD (Kingston SSDNow V+100 96 GB - miodzio). Bardzo dziękuję za docenienie takiego szaraczka jak ja :) Mam nadzieję, że będę miał szansę się wyróżnić (i zasłużyć na wyróżnienie:P) oraz na to, aby zaskoczyć zarówno czytelników dobrychprogramów jak i Redakcję :)* 

Kingston SSDNow V+100 96 GB - to nie jest recenzja

Nie chce się powtarzać pisząc recenzję dysku SSD, którą zrobił już wcześniej [Ave5](http://www.dobreprogramy.pl/Ave5/Kingston-SSDNow-V-GB-Recenzja,24691.html) /pozdrawiam %) /. Różnica jest jedynie w większej pojemności.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-11-10-_161_/g_-_608x405_-_-_28601x20111110201857_1.jpg)



Ten wpis chciałbym poświecić konfiguracji dysku pod Windowsami. Ze względu na to, iż charakterystyka SSD wymusza pewnie działa, które dla dysku HDD nie miałyby sensu, a nawet powodowałyby spadek wydajności. Zanim jednak przejdę do optymalizacji...



Krótko dodam kilka spostrzeżeń, odnośnie dysku SSD. Podczas zwykłem pracy, nie czuć przycięć i charakterystycznego dla dysków HDD, doczytywania danych, przy dużej fragmentacji. Laptop, w którym zmieniłem dysk na SSD wyraźnie dostał skrzydeł. A także to co jest ważne, praca stałą się przyjemniejsza dzięki temu, iż dysk SSD nie jest praktycznie słyszalny. Miłym plusem jest też również mniejszy pobór prądu.  Obecnie cena poniżej 600zł za 96GB trochę jeszcze odstrasza. Jeśli owe dyski potanieją, można będzie spokojnie polecić je do pracy np. w urządzeniach przenośnych. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-11-10-_161_/g_-_608x405_-_-_28601x20111110201857_2.jpg)



Dysk zmieniany był w czteroletnim laptopie z serii A200-1MD od Toshiby (Vista 32bit, Intel Core 2 Duo T5300, 2 GB RAM, zintegrowana grafika na chipsecie Intel 945).Stary dysk (HITACHI 160GB HTS541616J9SA0 5400 RPM) miał ranking wydajności dla dysku  na poziomie ok. 4, zaś nowy Kingston SSDNow uzyskał dokładnie 5.9 punktu. Całkiem ładny wynik.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-11-10-_161_/g_-_608x405_-_-_28601x20111110201857_3.jpg)



Jakby ktoś kiedyś zmieniał w tej serii dysk, to podpowiem, iż zaślepka A ukrywa stary dysk i tam właśnie należy wstawić nowy. W zaślepce B (aby otworzyć trzeba dość energicznie szarpnąć, zatrzaski siedzą bardzo mocno), wg instrukcji, również można umieścić dysk, jednakże, nie ma go do czego podłączyć... :)

Ok. To tyle odnośnie dysku Kingston SSDNow V+100 96 GB. Teraz najważniejsza treść tego wpisu, czyli jak skonfigurować dysk SSD, aby działał nam szybko i jak najdłużej.


Dysk SSD z Windows - konfiguracja (dlaczego?) 

Dyski SSD składają się z komórek NAND flash. Każda z nich ma określoną żywotność. Ogólnie dostępne dyski mają żywotność komórek na poziomie 10 000 cykli. Obliczono (teoretycznie), że dla użytkownika, który dość mocno obciąża system operacjami odczytu/zapisu, dysko SSD starczy na ok 100 lat. Wydaje się to bardzo długo. Ale, pamiętajmy, że klasyczne dyski HDD mają żywotność o wiele dłuższą, a zdążają się pady już po kilku latach. Tym bardziej, należy Windows odpowiednio przygotować  do pracy z SSD. Źle zoptymalizowany system może znacznie skrócić żywotność. 

Dodatkowo warto pamiętać, że najbardziej mordercze dla SSD są operacje nadpisywania, które wykonują dwie operacje: usunięcie starych danych w komórce i zapis nowych danych. Dzięki technologiom takim jak Wear Leveling i TRIM, służącąm do równomiernego wykorzystania każdej z komórek NAND i zarządzania zapisem, żywotność dysku wzrasta.

Warto dlatego, we własnym zakresie, skonfigurować system pod SSD tak, aby ilość operacji była jak najmniejsza. Charakterystyka dysków powoduje również to, iż niektóre aplikacje nie mają racji bytu, a tylko skracają żywotność dysku SSD. Przykładowo  programy do defragmentaryzacji należy dezaktywować, gdyż na dyskach SSD nie występuje fragmentaryzacja danych zmniejszająca czas dostępu (brak mechaniki dysku jak w przypadku HDD).

Dysk SSD z Windows - konfiguracja (do dzieła!) 

 *(Windows 7 wykrywa automatycznie dysk SSD i część poniższych kroków powinna być już wykonana automatycznie)* 



## Wyłączenie automatycznej defragmentaryzacji




Defragmentaryzację można nazwać zabójcą dysków SSD. Aby wyłączyć opcję, która automatycznie porządkuje dane, powinniśmy (na każdym z dysków) we Właściwościach wybrać zakładkę Narzędzia, a następnie przycisk Defragmentuj i Konfiguruj harmonogram. Odznaczamy checkbox Uruchom zgodnie z harmonogramem. Potwierdzamy przyciskiem Ok



## Wyłączenie indeksowania plików




W dysku SSD, czas dostępu do plików jest stały, a zatem indeksowanie również nie ma sensu. Aby wyłączyć usługę należy:
kliknąć prawym na Komputer i  wybrać Zarządzaj. Z drzewka po lewej wybieramy: Usługi i aplikacje a następnie Usługi, znajdujemy usługę Windows Search. Wybieramy właściwości i w nowo otwartym oknie ustawiamy typ uruchamiania na Wyłączony.



## Wyłączenie Superfetch




Kolejnym narzędziem zbędnym i powodującym niepotrzebne operacje na dysku, jest usługa Superfetch do optymalizacji uruchamianych aplikacji podczas startu Windows. Aby ją wyłączyć ją  należy podobnie jak wyżej wejść do usług i znaleźć usługę Wstępne ładowanie do pamięci, ją również należy wyłączyć.

To jeszcze nie jest koniec, aby pozbyć się "złej" usługi należy otworzyć Rejestr (uruchomić regedit.exe) i przejść do gałęzi:
HKEY_LOCAL_MACHINE -> System -> CurrentControlset -> Control -> Session Manager -> Memory Management -> PrefetchParameters. 
W tym miejscu po prawej stronie dla parametrów:
EnablePrefetcher
EnableSuperfetch
EnableBootTrace (jeśli jest)
ustawiamy wartość 0 (zero).




## Wyłączenie opróżnienia buforowania zapisu




Aby przejść do kolejnego kroku otwieramy Menedżer urządzeń poprzez kliknięcie prawym klawiszem myszy na Komputer, wybieramy Menedżer urządzeń.
W otwartym oknie z drzewka wybieramy Stacje dysków i nasz dysk SSD. W oknie otwieramy Właściwości i przechodzimy na zakładkę Zasady. Tam zaznaczamy oba checkboxy: Włącz buforowanie... i Wyłącz opróżnianie.... Potwierdzamy klikając przycisk Ok.




## Włączenie TRIM (tylko Windows 7)




Aby upewnić się, iż Windows 7 aktywował TRIM musimy skorzystać z wiersza poleceń (uruchomić cmd.exe). W konsoli wpisujemy:

 *fsutil.exe behavior query DisableDeleteNotify* 


Jeśli wartość ustawiona jest na zero, mamy pewność, że TRIM działa, w przeciwnym wypadku uruchamiamy go wpisując: 

 *fsutil.exe behavior set DisableDeleteNotify 0* 





## Przesunięcie sektora startowego (tylko Windows XP)




Podczas tworzenia partycji systemowej pod XP, system źle dobiera początek klastra NTFS, który znajdzie się pośrodku stron SSD. Aby temu zapobiec należy ściągnąć program Diskpart (w wersji 6+). Uruchamiamy program diskpart.exe i w konsoli wpisujemy:

sprawdzamy, który z naszych dysków jest SSD (jeśli mamy tylko SSD będzie on miał nr 1)

 *list disk* 


Wybieramy dysk SSD

 *select disk 1* 


UWAGA! Czyścimy dysk! 

 *clean* 

create partition primary align=1024
active
format fs=ntfs quick
exit

Nasza partycja jest gotowa na obsłużenie dysku SSD bezproblemowo.



## Tryb hardcore




Jeśli chcecie maksymalnie zminimalizować zapis/odczyt na nowym dysku SSD, warto skorzystać z poniższych wskazówek.



### Wyłączenie Hibernacji




Jeśli nie będzie to przeszkadzać, można wyłączyć Hibernację. Uruchamiamy wiersz poleceń  (cmd.exe) i wpisujemy: 

powercfg.exe -h off




### Pamięć wirtualna




W tym momencie mamy dwie drogi. 

Pierwsza, dla osób tylko z jednym dyskiem (oczywiście SSD): jeśli komputer ma więcej pamięci RAM niż 4GB (Vista) można pokusić się o wyłączenie pamięci wirtualnej (osobiście nie polecam tego, gdyż może czasem mocno spowolnić system). 
Otwieramy Właściwości systemu, przechodzimy na zakładkę Zaawansowane  i w polu Wydajność wybieramy Ustawienia. W nowo otwartym oknie przemieszczamy się na zakładkę Zaawansowane i klikamy na Zmień. W oknie Pamięć wirtualna: odznaczamy checkbox Automatycznie zarządzaj rozmiarem... i dla każdego dysku zaznaczamy Bez pliku stronicowania. Zatwierdzamy całość przyciskiem Ok

Druga ścieżka dla osób, które prócz systemowego dysku SSD mają jeszcze klasyczny dysk HDD. W tym przypadku pamięć wirtualną warto przenieść na dysk HDD. A zatem podobnie jak wcześniej przechodzimy do okna Pamięć wirtualna i odznaczamy checkbox Automatycznie zarządzaj rozmiarem....  Teraz możemy wybrać dysk HDD i zaznaczyć Rozmiar niestandardowy wpisując w obu polach rozmiar pamięci RAM przemnożony przez 1.5.



### Zmienne środowiskowe




Całkiem niegłupim pomysłem jest przeniesienie folderów typu Temp na dysk HDD (jeśli takowy jest). Otwieramy Właściwości systemu, przechodzimy na zakładkę Zaawansowane  i wybieramy Zmienne środowiskowe. W otwartym oknie w zmiennych użytkownika i systemowych przenosimy zmienne typu TEMP i TMP na dysk HDD.



### Włączenie trybu AHCI




Warto na koniec, wspomnieć o możliwości włączenia trybu AHCI (Advanced Host Controller Interface) dla dysku SSD, w celu optymalizacji zarządzania dyskiem. W tym celu w BIOSIe w Integrated Peripherals ustawiamy tryb na AHCI. Warto to zrobić przed instalacją systemu.




##  Podsumowanie 



Liczę na to, że mały poradnik, o tym jak zoptymalizować dysk SSD pod Windowsem, okaże się przydatny i pozwoli pracować dla waszych dysków SSD przez wiele pięknych lat ;)

 * Dziękuję i Pozdrawiam* 