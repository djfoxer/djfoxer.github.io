---
layout:     post
title:      Opera Mobile na Windows Phone
date:       2012-11-19 17:38:00
summary:    Windows Phone posiada jedyną słuszną przeglądarkę, czyli Internet Explorera w wersji mobilnej. Pomimo tego, iż IE na WP jest naprawdę świetną przeglądarką, każdy tęskni za czymś innym i lepszym. Tak powstał między innymi UC Browser,  czyli alternatywna przeglądarka do internetu (polecam sprawdzić!). Oczywiście nadal brakowało "króla" przeglądarek mobilnych, czyli Opery. Ktoś postanowił wziąć spraw...
categories: internet porady urządzenia mobilne
slug: Opera-Mobile-na-Windows-Phone,37367.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232819_0.jpg
---



Windows Phone posiada jedyną słuszną przeglądarkę, czyli Internet Explorera w wersji mobilnej. Pomimo tego, iż IE na WP jest naprawdę świetną przeglądarką, każdy tęskni za czymś innym i lepszym. Tak powstał między innymi [UC Browser](http://www.windowsphone.com/en-in/store/app/uc-browser/edd78a1a-7d08-4d56-abc0-d193db3a0984),  czyli alternatywna przeglądarka do internetu (polecam sprawdzić!). Oczywiście nadal brakowało "króla" przeglądarek mobilnych, czyli Opery. Ktoś postanowił wziąć sprawy w swoje ręce...



### Opera Mobile na Windows Phone 7.5



Pod koniec 2011 roku na XDA-Developers pojawiła się Opera Mobile na Windows Phone. Był to tak naprawdę port z poczciwego Windows Mobile. Pamiętamy oczywiście, iż Windows Phone 7.x bazują w linii ciągłej na starym systemie mobilnym + środowisko uruchomieniowe w Silverlight. Ze względu na to, iż był to pliki exe z odpowiednią warstwą do otwarcia na naszym systemie, wymagane było posiadanie pełnego odblokowania. Na to mogły sobie pozwolić jedynie urządzenia z custom romem. Aż do teraz...




### WP7 Root Tools 0.12 - uruchamianie natywnych aplikacji!



W tym tygodniu pojawiła się, wreszcie dług oczekiwana, aktualizacja do [WP7 Root Tools 0.12](http://www.wp7roottools.com/).  Prócz dodania kilku tweaków do systemu, instalacji certyfikatów i spolszczenia, otrzymujemy także... możliwość uruchamiania natywnych aplikacji (exe)!

Dzięki temu, bez podmiany romu, możemy poprzez WP7 Root Tools, "aktywować" aplikację i biblioteki, które będą działały w trybie natywnym. Jest to o tyle ważne, iż do tej pory wgranie custom romu nie było możliwe na wszystkich urządzeniach. Co więcej, nie zawsze proces był prosty, a i istniało ryzyko uszkodzenia sprzętu. 

Obecnie wystarczy mieć odblokowanie interop i ściągnięte [WP7 Root Tools 0.12](http://www.wp7roottools.com/).  W przypadku Opera Mobile, należy pobrać z forum XDA plik [OperaMobile10_ForAllUnlocks](http://forum.xda-developers.com/showthread.php?t=1410643),  zainstalować xap i nadać prawa roota. Dla tej ostatniej czynności, wystarczy w WP7 Root Tools wejść na zakładkę  *Uprawnienia*  i dla Opery aktywować przełącznik. W tym momencie zostaną przetworzone pliki wykonawcze i biblioteki aplikacji, aby mogły zostać uruchomione z podwyższonymi uprawnieniami (UWAGA! Proces może potrwać do kilku minut).


W taki oto prosty sposób dostaliśmy działającą Opera Mobile na Windows Phone, bez wgrywania custom romu. Co ciekawe, w przyszłości autor WP7 Root Tools, planuje dodać instalację sterowników m.in do przesyłania przez bluetooth.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232819_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232825_0.jpg)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232830_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232834_0.jpg)





### Opera Mobile na Windows Phone - trochę ponarzekajmy



Początki bywają trudne i w tym przypadku jest podobnie. Ze względu na to, iż jest to port z Windows Mobile, otrzymujemy wersję zaledwie 10. Niestety czuć to. 

Część stron nie wyświetla się do końca poprawnie. Na przykładzie witryny dobrychprogramów, można zauważyć problem z cssami (kolumny). Co więcej brak obsługi HTML5 sprawia, iż nie uświadczymy żadnych funkcji, jak choćby filmów osadzonych na stronach. Można również czasem zauważyć błędy w wyświetlaniu tabel, szczególnie widać to przy powiększeniu.


Będąc przy powiększeniu. Otóż ta wersja Opery nie obsługuje wielodotyku, a zatem "uszczypnięcia" nie pomniejszą/powiększą strony. Jedyna opcja to staromodne  "stukanie" w stronę lub przycisk zoom. 

Idąc dalej. Brak obracania obrazu, to już większa bolączka, choć podobno autor ma ją wyeliminować w nowej wersji. Z wad wymienię jeszcze to, iż nie posiadamy możliwości zmiany trybu pracy z wersji mobilnej na stacjonarną. Przez co, niektóre strony wyświetlane są w wersji pod komórki i nic nie możemy niestety z tym zrobić. Bolesne jest również brak cofania przy pomocy przycisku wstecz na obudowie. Niestety.

Na koniec jeszcze ciekawostka. Ta wersja Opery, ma tendencję do znikania... Niby istnieje w pamięci (ponownie otwarcie przywraca aplikację do wcześniejszego stanu), ale nie ma jej w procesach (rootkit? :P )



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232946_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232907_0.jpg)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121117001818_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232927_0.jpg)





### Opera Mobile na Windows Phone - a jednak są i małe plusy



Zacząłem od wad, ze względu na to, iż są najbardziej rzucające się w oczy. Port Opery ma jednak i sporo zalet. Warto na początek zaznaczyć, iż jest to w sumie pełni działająca Opera Mobile. O dziwo jest ona całkiem szybka, jak na tego typu aplikację. Pomimo problemów z zoomem, strony przegląda się całkiem przyjemnie. Nawet archaiczny interfejs (dwa paski na dole i góry ekranu) nie jest uciążliwy.

W "zestawie" dostajemy opcję, których próżno szukać w IE na Windows Phone. Mamy tu zatem wyszukiwanie po stronie, działające świetnie. Co jeszcze? Pobieranie plików, bez względu na typ (z możliwością wyboru miejsca pobrania). Dodatkowo możemy zapisywać w cacheu strony www i później przeglądać je offline. Kolejny miły dodatek z Opery.

Nadal jednak przeszkadza to, iż część stron ma problemy z wyświetlaniem kolumn. Nowa wersja WP7 Root Tools, pozwalająca uruchamiać aplikacje natywne, przyczyni się to zapewne do ulepszenia portu Opery. Teraz jeszcze więcej osób będzie w stanie zainstalować ją, a co za tym idzie, autor portu, będzie miał dla kogo tworzyć lepsze wersje. Jest jeszcze sporo do naprawienia, ale potencjał jest spory. Szkoda, tylko, że to ostatnia wersja Opery Mobile na Windows Mobile, a zatem samo renderowanie nic się zapewne nie zmieni. 

Jednakże moc drzemiąca w WP7 Root Tools może nas jeszcze zaskoczyć i nie skończy się tylko na Operze, ale dostaniemy też inne porty z Windows Mobile. Szczególnie, że chodzą słuchy, iż WP7 Root Tools już jest testowany pod Windows Phone 8 (oparty jest o linię NT, a za tym idzie jeszcze więcej możliwości!). Obecnie Opera jest ciekawostką i próbą tego, co można wrzucić na Windows Phone, a o czym nigdy nie pomyśleliby twórcy systemu. Polecam sprawdzić jak zachowuje się port, jednej z popularniejszych przeglądarek mobilnych. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232839_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232846_0.jpg)






![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232932_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232936_0.jpg)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232941_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-11-19-_131_/g_-_-x-_-_-_x20121116232901_0.jpg)

