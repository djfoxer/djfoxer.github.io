---
layout:     post
title:      Polski Windows Phone 7.5 Mango (aktualizacja) i Marketplace via Zune
date:       2011-09-30 07:55:00
summary:    Po wielu bojach zainstalowałem już na swoim LG E900 Windows Phone 7.5 Mango, nie czekając na patcha ze strony Microsoftu/LG. Jeśli kogoś to interesuje zapraszam do wątku — http — //answers.microsoft.com/en-us/winphone/forum/wp7-sync/lg-e900-upd... W tym malutkim wpisie pragnę przedstawić — 1. Jak zaktualizować swój telefon z Windows Phone 7 do wersji 7.5 Manogo w pełni spolszczonej (klawiatura, interfac...
categories: windows sprzęt urządzenia mobilne
slug: Polski-Windows-Phone-7.5-Mango-aktualizacja-i-Marketplace-via-Zune,28084.html
---



Po wielu bojach zainstalowałem już na swoim LG E900 Windows Phone 7.5 Mango, nie czekając na patcha ze strony Microsoftu/LG. Jeśli kogoś to interesuje zapraszam do wątku:
[http://answers.microsoft.com/en-us/winphone/forum/wp7-sync/lg-e900-update-error-code-8018001e/1ec8d54d-0ee8-4db6-ab62-4ca26b3fbbe7](http://answers.microsoft.com/en-us/winphone/forum/wp7-sync/lg-e900-update-error-code-8018001e/1ec8d54d-0ee8-4db6-ab62-4ca26b3fbbe7)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-9-30-_167_/g_-_608x405_-_-_28084x20110929233142_1.png)
 

W tym malutkim wpisie pragnę przedstawić:
1. Jak zaktualizować swój telefon z Windows Phone 7 do wersji 7.5 Manogo w pełni spolszczonej (klawiatura, interface, pomoc, słownik itd.). Cały proces należy wykonać PRZED aktualizacja do wersji 7.5, gdyż po aktualizacji nie będzie już możliwe zainstalowanie pełnej polskiej wersji.

2. Jak w pełni, cieszyć się zakupami w Marketplace poprzez Zune w języku polskim - opisy, ceny, zakupy aplikacji i gier.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-9-30-_167_/g_-_608x405_-_-_28084x20110929233142_3.JPG)
 

 *Cel 1. - Aktualizacja Mango do PL* 

Mimo, że nic zbytnio nie można tu zepsuć. Robicie to na własną odpowiedzialność. 

Aby wykonać ten krok, niezbędne będzie małe "grzebanie" w rejestrze. Naszym celem będzie utworzenie w korzeniu HKEY_LOCAL_MACHINE podgałęzi: MUI\Available. W tej podgałęzi należy utworzyć klucz: 0415, o wartości Polish. 

W ten prostu sposób, gdy zainstalujemy Windows Phone 7.5 Mango, nasz smartfon będzie posiadał pełną, polską wersję językową!


 *Zmiana w LG E900* 

Posiadacze telefonów od LG, dostali świetną aplikację MFG do zarządzania telefonem. Każdy posiadacz LG ma ją u siebie zainstalowaną, tylko ukrytą.  Jest to swego rodzaju program serwisowy. Dzięki niej bez niczego możemy odblokować system, ustawić tethering – udostępnianie internetu przez USB, przetestować system, pogrzebać w rejestrze i wiele wiele innych opcji. 

Oto co musimy zrobić by osiągnąć założony cel:
- dzwonimy na numer ##634# (w taki oto sposób aktywujemy aplikacje MFG, później będzie ona już dostępna z listy aplikacji)
- jako hasło wpisujemy: 277634#*#
- przechodzimy do edycji rejestru wybierając: 7 (Engineer Menu) ->  6 (Other Setting) -> Edit registry
- będąc w menu rejestru ustawiamy:
1.
Select ROOT_PATH - HKEY_LOCAL_MACHINE
2. 
Input SUB_PATH - MUI\Available
3. 
Input KEY - 0415
Select data type - String
4. 
Input data (Just needed in Set) - Polish

Przyciskamy Set i już. Można jeszcze przyciskiem Query sprawdzić czy zapis się udał.


 *Zmiana w pozostałych modelach* 

Niestety w pozostałych model, aby zmienić wartość rejestru należy zainstalować  Registry Editor for Windows Phone 7 ([http://forum.touchxperience.com/viewtopic.php?f=20&t=593](http://forum.touchxperience.com/viewtopic.php?f=20&t=593)). Piszę niestety, gdyż aby to zrobić trzeba odblokować telefon. Jak to zrobić? Na pewno znajdziecie. Nie o tym jest ten wpis.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-9-30-_167_/g_-_608x405_-_-_28084x20110929233142_2.png)
 

 *Cel 2. - Marketplace PL poprzez Zune * 

Aby móc wejść poprzez Zune do Marketplace i móc robić zakupy (inaczej pojawi się alert, iż opcje regionalne na komputerze nie zgadzają się z opcjami na koncie Live), musimy przeprowadzić kilka kroków, które pozwolą nam cieszyć się w pełni z naszego polskiego Marketplace:

1. W systemie nasza lokalizacja (zmieniamy w Panelu Sterowania) musi być ustawiona na: "Polska"  (jeśli mamy polski system nie musimy najprawdopodobniej tego robić)

2. Logujemy się na nasze konto Windows Live [https://signup.live.com/](https://signup.live.com/). Tam musimy ustawić nasz region na "Polska":
- przechodzimy do opcji konta: [https://account.live.com/summarypage.aspx](https://account.live.com/summarypage.aspx)
- przy polu "Country/region" wybieramy "Change"
- z rozwijanej list "Country/region" wybieramy "Poland"
- zapisujemy klikając na "Save"

3. Ostatni krok, o którym nie wiedzą wszyscy. Tworząc konto na Windows Live, mamy również zakładane konto na XBOX Live. Tu musimy migrować nasze konto do Polskiego XBOX Live.
- wchodzimy na link do migracji: [https://live.xbox.com/pl-PL/BillingMigration/SelectRegion](https://live.xbox.com/pl-PL/BillingMigration/SelectRegion)
- kreator sprowadza się do wybrania regionu "Polska" i potwierdzenia tego w kilku krokach

 *Witam w polskim Windows Phone 7.5 Mango i Marketplace!* 

W taki oto prosty sposób możemy: zainstalować aktualizację Mango do Windows Phone z pełną, polską wersją językową systemu (Cel 1.) oraz w Marketplace.  poprzez w Zune, logować się i robić zakupy (Cel 2.).

W dwóch krokach, dzięki Mango (Tak na marginesie - świetny update i naprawdę warto było czekać na tą aktualizację! Jeśli planowałeś kupić smartfone z Windows Phone, teraz jest świetna okazja by to zrobić! Więcej wkrótce...), z małą pomocą, otworzyliśmy drzwi do świata Windows Phone w całości w języku polskim!! :D



 * Dziękuję i Pozdrawiam* 







Powiązane:
[Windows Phone 7.5 Mango - (R)EWOLUCJA?](http://www.dobreprogramy.pl/djfoxer/Windows-Phone-Mango-REWOLUCJA,28224.html)
[Windows Phone 7 w LG E900](http://www.dobreprogramy.pl/djfoxer/Windows-Phone-w-LG-E,26695.html)


