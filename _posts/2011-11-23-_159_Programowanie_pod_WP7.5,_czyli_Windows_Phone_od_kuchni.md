---
layout:     post
title:      Programowanie pod WP7.5, czyli Windows Phone od kuchni
date:       2011-11-23 23:14:00
summary:    Po miesiącach szaleństw z Windows Phone, nieskończonej liczby instalacji i deinstalacji, kilku flashowaniach, grzebaniach się w MFG, aktualizacjach (udanych i tych zakończonych niepowodzeniem), przyszedł wreszcie czas, ażeby "spoważnieć" :P i napisać coś własnego na Windows Phone 7.5. Od razu napisz...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_7" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_7" checked="checked" value="128"><label for="chkTagsList_7">programowanie</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



Po miesiącach szaleństw z Windows Phone, nieskończonej liczby instalacji i deinstalacji, kilku flashowaniach, grzebaniach się w MFG, aktualizacjach (udanych i tych zakończonych niepowodzeniem), przyszedł wreszcie czas, ażeby "spoważnieć" :P i napisać coś własnego na Windows Phone 7.5. Od razu napisze, że jest kilka problemów (i to wcale nie natury programistycznej).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-11-23-_159_/g_-_608x405_-_-_28713x20150107205731_0.jpg)





## Dla kogo?



Chcący zacząć programować dla Windows Phone 7(.5) powinniśmy umieć "na dzień dobry" podstawy C#/VB oraz podstawy Silverlighta lub XNA jeśli zechcemy tworzyć gry (także na XBox360!). Aplikacje pisane są w Visual Studio 2010 for Windows Phone. W Tym krótkim przewodniku postaram się opisać jak zacząć przygodę z pisaniem aplikacji na Windows Phone. A zatem, do dzieła!




## Visual Studio 2010 for Windows Phone



Jak już wspomniałem przygodę rozpoczynamy od instalacji Visual Studio 2010 for Windows Phone [http://www.microsoft.com/visualstudio/en-us/products/2010-editions/windows-phone-developer-tools](http://www.microsoft.com/visualstudio/en-us/products/2010-editions/windows-phone-developer-tools). 

Aby móc uruchomić środowisko musimy mieć Windows 7  lub Windowsa Vista + SP2 (wszystkie edycji oprócz Starter). Jednakże osoby, które zechcą zainstalować IDE na XP nie będą na przegranej pozycji (częściowo, zobaczycie czemu). Otóż można zmusić pakiet do instalacji na nieśmiertelnym XP. Oto co należy zrobić:
 
1. Ściągamy normalnie Visual Studio 2010 for Windows Phone
2. Po ściągnięciu, ropakowujemy plik poleceniem vm_web2.exe /x
3. Przechodzimy do folderu gdzie wypakowały się pliki i szukamy pliku baseline.dat
4. Edytujemy go i szukamy sekcji gencomp7788
5. Szukamy dwóch wpisów 
InstallOnLHS=1
InstallOnWinXP=1
6. Zmieniamy je na 
InstallOnLHS=0
InstallOnWinXP=0
7. Zapisujemy plik i startujemy z instalacją poleceniem: setup.exe /web

Cały pakiet instaluje się normalnie, bez najmniejszych błędów. Jednakże jest to połowiczny sukces. Możemy pisać aplikacji i je kompilować, jednakże nie będzie działało debugowanie na emulatorze. Problemem jest brak wsparcia DirectX 10+ na XP. Śmieszne jest to, że tak naprawdę ten DirectX 10+ do niczego nie jest potrzebny (u mnie na Windows Vista całość śmiga mimo, że karta wspiera max DirectX 9.0c). Jest to kolejna próba uśmiercenia XP, takie czasy. Nie pomaga wgranie "zhackowanych" plików z DirectX 10. Jest jednak jedno wyjście. Możemy nasze programy debugować... na urządzeniu po wcześniejszym deployu (który wymaga odblokowania urządzenia, o czym dalej). Podsumowując: jakby ktoś mocno się uparł, może na XP odpalić Visual Studio 2010 for Windows Phone :)

Wracając do rzeczywistości. Z racji tego, że mam na laptopie Viste i instalowałem system od nowa, musiałem pobrać wszystkie aktualizacje, aż do SP2. Ściąganie poprawek trwało kilka godzin! Chcąc mieć SP2 trzeba mieć SP1, ale mając SP1 nie można przejść do SP2, tylko trzeba ściągnąć inne poprawki, w tym niewymagane, które mimo wszystko są wymagana do instalacji SP2, podobni było z SP1 blebleblalblabla, masakra... 

Po przejściu wymogów jakie stawienie są dal Visty, wreszcie zaczęła się instalacja VS (oczywiście też ściąganie z serwerów MS, ale tu już wszystko przebiegało automatycznie). Otrzymujemy w ten sposób jedno z najbardziej dopracowanych IDE :)

Teraz mała uwaga odnośnie działania emulatora. Otóż na moim leciwym już laptopie: Intel C2D T5300, 2GB RAM, zintegrowana grafika na chipie Intel 945, dysk SSD (tak, tak to ten z dobrychprogramów, dzięki :D ) VS działa bardzo szybko i płynnie. Jednakże odpalenie debugowania na emulatorze, powoduje zadyszkę (szczególnie na początku). Czuć, że przydało by się trochę więcej RAMu no i brak wsparcia sprzętowego dla sztucznie wciśniętego DricetX 10+ robi swoje. Jednakże trzeba zauważyć, iż sam emulator nie jest emulatorem systemu (jak ma to miejsce w przypadku iPhona i ich xcode), ale ale pełnym emulatorem urządzenia. Całkiem ciekawe rozwiązanie. Szkoda, że kosztem wydajności.

Mając już środowisko, chlelibyśmy zacząć coś pisać...




## Baza wiedzy



Z racji tego, iż temat programowania na Windows Phone 7 jest dość świeży, chętni znajdą wiele ciekawych poradników/książek z pomocą w kodowaniu online i nie tylko. 

Zaczynając od darmowych ebooków:
- Programming Windows Phone 7 (autor Charles Petzold, tego Pana większość pewnie kojarzy :D ) - [http://www.charlespetzold.com/phone/](http://www.charlespetzold.com/phone/)
- Silverlight for Windows Phone Toolkit In Depth (Boryana Miloshevska) [http://windowsphonegeek.com/WPToolkitBook](http://windowsphonegeek.com/WPToolkitBook)
- Windows Phone Programming in C# (Windows Phone Version 7.5) (Rob Miles) [https://www.facultyresourcecenter.com/curriculum/pfv.aspx?ID=8874&c1=en-us&c2=0&Login=](https://www.facultyresourcecenter.com/curriculum/pfv.aspx?ID=8874&c1=en-us&c2=0&Login=)

poprzez kursy online:
- Kurs programowania Windows Phone 7 
[http://channel9.msdn.com/Series/Kurs-programowania-Windows-Phone-7](http://channel9.msdn.com/Series/Kurs-programowania-Windows-Phone-7)
- Kurs programowania Windows Phone – pisz na Mango
[http://channel9.msdn.com/Series/Kurs-programowania-Windows-Phone-pisz-na-Mango](http://channel9.msdn.com/Series/Kurs-programowania-Windows-Phone-pisz-na-Mango)
- Windows Phone 
[ http://msdn.microsoft.com/pl-pl/library/hh150095.aspx](http://msdn.microsoft.com/pl-pl/library/hh150095.aspx)

i wydania książek w języku polskim:
- Windows Phone 7. Tworzenie efektownych aplikacji (Henry Lee, Eugene Chuvyrov) [http://helion.pl/ksiazki/windows-phone-7-tworzenie-efektownych-aplikacji-henry-lee-eugene-chuvyrov,winph7.htm](http://helion.pl/ksiazki/windows-phone-7-tworzenie-efektownych-aplikacji-henry-lee-eugene-chuvyrov,winph7.htm)

W sieci jest tego bardzo dużo, zainteresowani tematem znajdą tego, całkiem sporo. Przypominam, także o konkursie "Zgarnij telefon z Windows Phone w GeekClub" ([http://www.codeguru.pl/static/WP7](http://www.codeguru.pl/static/WP7)), gdzie po opublikowaniu 5 aplikacji na Windows Phone Marketplace, można wygrać samrtfon z Windows Phone 7.5.

Aplikacja gotowa, chcę wrzucić ją na własnego smartfona...




## Odblokowanie telefonu



Jak już wiadomo, jedną z możliwości odblokowania telefonu jest zakup konta na AppHubie. Nie jest to jednak jedyna, oficjalna, droga na wgranie oprogramowania na komórkę w plikach xap (format plików na Windows Phone). 

Swego czasu, po premierze Windows Phone w roku 2010, stworzono aplikację Chevron. Dzięki niej, możliwe było odblokowanie telefonu całkowicie za darmo. Oczywiście, jak można się domyśleć, Microsoftowi nie było to na rękę. Zrobił on jednak ciekawy krok. Programistów, odpowiedzialnych za stworzenie Chevrona, wziął pod własne skrzydła. Tak oto powstał projekt ChevronWP7 ([http://www.chevronwp7.com/](http://www.chevronwp7.com/)). Dzięki niemu za 9$, każdy jest w stanie odblokować swój telefon (ściągnięcie aplikacji ChevronWP7, podpięcie telefonu do komputera, zapłacenie za token do odblokowania i  praktycznie mamy odblokowany smartfon). Bardzo ciekawa inicjatywa i nie jest wcale bardzo kosztowna, a umożliwia wrzucanie aplikacji z poza oficjalnego źródła. Mimo małej przerwy w odblokowaniu urządzeń, obecnie nie występują żadne utrudnienia.

Jest jeszcze droga nieoficjalna. Jednakże po aktualizacji do Mango, stała się ona utrudniona. Otóż Chevron nie działa na najnowszej wersji WP. Są różne sposoby, jednakże nie działają one na wszystkich urządzeniach. Jeśli ktoś jest zainteresowany, z pewnością znajdzie je w sieci.

Mam już coś stworzonego i przetestowanego na własnym smartfonie, jak pokazać to światu...




## AppHub i Marketplace




Marketplace jest miejscem, gdzie wrzucamy nasze gotowe aplikacje, a każdy użytkownik Windows Phone 7 może je pobrać. Aby to zrobić należy założyć konto na stronie AppHub ([http://create.msdn.com](http://create.msdn.com)), gdzie wrzucamy gotowe programy.

Mamy możliwość założenia trzech typów konta:

- STUDENT - darmowe założenie konta, brak jakichkolwiek opłat. Aby to zrobić należy zarejestrować LiveID w usłudze DreamSpark ([www.dreamspark.com](www.dreamspark.com), uczelnia musi uczestniczyć w tym programie);  możliwość odblokowania 1 urządzenia

- OSOBA PRYWATNA - brak działalności gospodarczej; opłata 99$ za rok; możliwość odblokowania 3 urządzeń

- FIRMA - działalność gospodarcza; opłata 99$ za rok; możliwość odblokowania 3 urządzeń

Wszystkie konta mają brak limitu na płatne aplikacje. Jedyny limit to 100 darmowych aplikacji, potem 19,99$ za kolejne.

Dzięki rejestracji (aktywacja trwa do 10 dni, bywają problemy z kontami płatnymi), możemy publikować aplikacje do Marketplace (płatne i darmowe). Dodatkowo uzyskujemy możliwość odblokowania telefonu i publisha aplikacji bezpośrednio do urządzenia.

Kolejny krok to weryfikacja programu, który chcemy wrzucić do Marketplace. Przesyłamy nasz program do Microsoftu i tam, w ciągu 5 dni otrzymujemy informację o wyniku tego etapu. Aplikacja może zostać odrzucona ze względu na uwagi od strony technicznej (np. złe wykorzystanie GPS), czy ze względu na treść (np. emulator gier na NES z ROMem).

Program płatny może kosztować najmniej 0.99$, zaś najdroższy 499$.
Kiedy nasza aplikacja osiągnie sukces komercyjny warto wiedzieć coś o podziale zysków. Otóż Microsoft bierze 30% dochodu, a 70% dostaje twórca. Aby móc odebrać pieniądze należy wysłać druk W8B do MS. Dodatkowo, gdy zechcemy płacić podatek w Polsce (potrącany w USA), należy wyrobić numer ITIN (Individual Taxpayer Identification Number).

Więcej szczegółów na : [http://create.msdn.com/en-US/home/faq](http://create.msdn.com/en-US/home/faq)







##  Podsumowanie 



Mam nadzieję, że ten krótki wpis zainteresuje część osób do pisania aplikacji na Windows Phone, a także wyjaśni kilka zawiłości w temacie.

 * Dziękuję i Pozdrawiam* 