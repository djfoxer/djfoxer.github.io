---
layout:     post
title:      Fakty i mity o Windows Phone
date:       2012-06-19 18:05:00
summary:    W jednym z komentarzy na portalu, WODZU podał link do blogu, ze zbiorem kilkudziesięciu (dokładnie 75) bolączek jakie ma Windows Phone wg autora strony. Po przejrzeniu kilku z nich, okazało się, że część z nich jest faktycznie prawdą. Jednakże, dużo z tych "żali" jest albo pisana na siłę, albo nie ma nic wspólnego z faktami. Część osób zapomniała, iż Windows Phone nie ma nic wspólnego z kierunkiem...
categories: oprogramowanie porady urządzenia mobilne
---



W jednym z komentarzy na portalu, [WODZU](http://www.dobreprogramy.pl/WODZU) podał link do blogu, ze zbiorem kilkudziesięciu (dokładnie 75) bolączek jakie ma Windows Phone wg autora strony. Po przejrzeniu kilku z nich, okazało się, że część z nich jest faktycznie prawdą. Jednakże, dużo z tych "żali" jest albo pisana na siłę, albo nie ma nic wspólnego z faktami. 

Część osób zapomniała, iż Windows Phone nie ma nic wspólnego z kierunkiem w jakim idzie Android. Windows Phone jest umiejscowiony w segmencie razem z iPhonem, stąd mają one wiele wspólnych rozwiązań (i ograniczeń). To nie Windows Mobile, w którym można było robić niemalże wszystko. Niektóre zarzuty, nie biorą pod uwagę tego założenia.

Postanowiłem, skomentować te punkty (pisownia oryginalna) i umieścić je na blogu (źródło pytań nie ma znaczenia, a odpowiedzi nie mają konkretnego adresata). Odpowiedzi starałem się pisać w miarę rzetelne. Jeśli, gdzieś jest błąd/niespójność lub można coś dodać, proszę gorąco o zwrócenie uwagi. Zapraszam do lektury i wyrażenia swojej opinii. 

Ze względu na premierę Windows Phone 8 i Windows Phone 7.8, wpis został zaktualizowany. Tam, gdzie zaszły zmiany względem nowej wersji systemu dodałem odpowiednie komentarze.










### 1.	Brak prawdziwego multitaskingu. Po wyjściu z programu jest on wyłączany. Najbardziej okrutnie to widać w przypadku różnego rodzaju komunikatorów.

Nie jest to multitasking znany choćby z systemów desktopowych. Windows Phone "hibernuje" aplikację. Jednakże nie jest tak, że nic nie może działać w tle. Otóż w tle mogą działać tzw. agenci, uruchamiani co 30 minut na jakiś krótki okres czasu (idealne do np. aplikacji pogodowych). Istnieją również agenci, uruchamiani przy określonych warunkach (połączenie z WiFi, ładowanie itp.), do działań związanych np. z synchronizacją. To nie koniec, możemy użyć gotowych agentów wyspecjalizowanych do odtwarzania muzyki lub transferu plików działających w tle i nie mających tych ograniczeń ([więcej w tym linku](http://weblogs.asp.net/jgalloway/archive/2011/11/23/leveraging-background-services-and-agents-in-windows-phone-7-mango.aspx)). Jeśli chodzi o komunikatory, to ewidentnie jest to nietrafiony przykład! Otóż istnieją notyfikacje typu push, które nie wymagają nawet otwartej aplikacji. Np. komunikator [Pogaduszki](http://www.windowsphone.com/pl-PL/apps/db95b884-46be-42de-9233-258ccc07f47d) lub [GG](http://www.windowsphone.com/pl-pl/apps/81fa3f08-d030-42ba-b36c-37b95908b6d7) nie muszą być włączone, aby odbierać wiadomości w tle. Jeśli przyjdzie do nas wiadomość, otrzymamy informację na ekranie głównym. Oczywiście, nic nie dzieje się bez naszej zgody. Lista aplikacji działających w tle dostępna jest w ustawieniach. Nie ma tu miejsca na ukrycie działania jakiejś aplikacji. Wszystko jest jasne i klarowne.





### 2.	Brak trybu pamięci masowej. Sorry.
3.	Brak obsługi kart pamięci. W ten sposób też nie prześlesz plików.

Tryb pamięci masowej można uruchomić poprzez prostą aplikację (jeden przycisk "aktywuj") [USB Storage Enabler](http://forum.xda-developers.com/showthread.php?t=1069568). Co innego, że taki tryb w obecnych czasach jest mało przydatny. Pendrive 16GB można kupić za 30zł. Większość z nas ma dostęp do sieci, wrzucenie plików poprzez np. SkyDrive jest naprawdę szybkie i wygodne.

 *Windows Phone 8* 

WP8 posiada tryb pamięci masowej.


### 4.	Brak menadżerów plików.

Windows Phone nie jest Androidem. Każda aplikacja pracuje w izolowanym środowisku, nie współdzieląc z sobą większości plików (poza np. zdjęciami umieszonymi w "Zdjęcia"). Dzięki czemu nie ma śmieci po odinstalowaniu programu, a także bezpieczeństwo stoi na znacznie wyższym, niedostępnym dla Androida poziomie. W takim przypadku menadżer plików nie ma zbytnio sensu. Każda aplikacja jest integralną częścią, a wspólne pliki przechowywane są jawne w hubbie (zdjęcia, muzyka). Zawsze można przesłać pliki do chmury, jak np. SkyDrive.

Jednakże dla urządzeń odblokowanych jest rewelacyjna aplikacja [WP7 Root Tools](http://www.wp7roottools.com/) z m.in. menadżerem plików i edytorem rejestru.

 *Windows Phone 8.1* 
 WP8.1 posiada menadżerów plików.


### 5.	Potrzebujesz Zune, żeby przesyłać pliki jednak Zune tylko przesyła zdjęcia, filmy i muzykę. Inne rodzaje plików musisz sobie chyba wysłać na maila, żeby mieć je na swoim telefonie.

Pliki przesyłać można spokojnie poprzez SkyDrive, który jest ściśle zintegrowany z systemem jak nigdzie indziej.


 *Windows Phone 8* 

Zune nie jest już potrzebne dla  WP8 (patrz punkt 3.).



### 6.	W tej chwili jest ograniczony do właściwie jednej rozdzielczości.

Zgadza się. I to jest piękne. Developerzy tworząc aplikację wiedzą jakiej rozdzielczości się spodziewać i mają ułatwione zadanie. Jeśli chodzi o użytkowników końcowych, to nie powinno oni mieć jakiś zastrzeżeń. 800x480 nawet na ekranach 4,3" wygląda świetnie. Zmieni się to jednak z premierą WP8, gdzie możliwe, że będą nowe rozdzielczości. Zobaczymy, jak będzie wyglądać to wówczas.

 *Windows Phone 8* 

Nowy system występuje w trzech rozdzielczościach: WVGA (480 x 800) obecna , WXGA (1280 x 768) i 720p (1280 x 720).


### 7.	Wyszukiwanie głosowe w tej chwili to tylko Bing (wszyscy wiemy jak on dobrze działa).

"wszyscy wiemy jak on dobrze działa" - tak, a jak? ;) Nie jest wcale tak źle, co innego, że nie używam tego zbytnio, a Wy (pytanie do tych co mają WP, a nie do tych co widzieli reklamę w tv :P )? 

 *Windows Phone 8.1*  WP8.1 - dodaje rewelacyjną Cortanę, asystentkę mowy!

 *Windows Phone 8* 

Nowy system dodaje możliwość wydawania poleceń w języku polskim oraz został ulepszony.



### 8.	Brak jakiegokolwiek sposobu do podłączenia się do jakiegokolwiek VPN-a. (I to ma być telefon biznesowy?)

Jest w Windows Phone 8.1. 


### 9.	Brak możliwości nagrywania rozmów (na prawdę telefon biznesowy?)

Brak. Ci z Bridgestone Australia to jacyś dziwni są, że wzięli Lumię 800 jako urządzenie flotowe. 


### 10.	Brak możliwości blokowania niechcianych połączeń.

Dodano w Windows Phone 8.


### 11.	Nie zsynchronizujesz maili bezpośrednio z komputerem bez wysyłania ich do chmury microsoftu.

Z tego co mi wiadomo, maile synchronizowane są poprzez konto, na którym się synchronizuje.



### 12.	System całkowicie zamknięty. Nigdy nie wiesz co tam siedzi w środku i czy przypadkiem nie ma jakichś furtek dla FBI/CIA.

O tak. Nigdy nie wiadomo :P Ale zaraz, czy to nie Android szpiegował użytkowników poprzez punkty WiFi? :P



### 13.	Brak możliwości zmiany wielkości czcionki systemowej.

Tak, ale w jakim celu? Wielkość jest ustalona poprzez założenia interfejsu Metro, dzięki czemu wszystko jest czytelne i nawet osoby starsze nie będą miały problemów z użytkowaniem.

 *Windows Phone 8* 

Dodano możliwość zmiany rozmiaru czcionki.



### 14.	Brak możliwości zmiany nazwy obrazków i zdjęć przy pomocy telefonu!

Taaa. Ale które pliki? System pliki trzyma lokalnie i na SkyDrive. Na SkyDrive zmieniać nazwy można. Na dysku lokalnym, system plików jest ukryty i zdjęcia/filmy/muzykę przesyła się  poprzez Zune, podczas synchronizacji. Po co tam są jakieś customizowane nazwy plików? Dla plików Office nazwy można zmieniać lokalnie. 


### 15.	Nie możesz zmienić kraju dla twojego Windows Live ID po ustawieniu.

Cóż, to już problem nie związany z Windows Phone, ale ogólnie z kontem Live ID. Podobnie oczywiście jest dla użytkowników X360, ale również Sony Vita ma ograniczenia dla kont (chociaż nie jest to analogiczne jak w Live ID, ale pokazuje, że ten "trend" jest globalny, czy to dobrze, czy źle to już inna sprawa)


### Aktualizacja

Od jakiegoś czasu można już mieniać kraj dla Live ID.


### 16.	Wygaszacz ekranu jest kompletnie czarny i nie może nic wyświetlać. (np Zegarek albo powiadomienia)

Ktoś nie zrozumiał jak to działa. Nie ma wygaszacza ekranu jak w desktopie. To urządzenie mobilne i jest blokada ekranu. Po zablokowaniu ekranu jest widoczna godzina, data, powiadomienia odnośnie poczty, sms, nieodebranych połączeń, wydarzeń z kalendarza. Co więcej, na odblokowanych urządzeniach można zainstalować Lock Widgets. Wówczas na ekranie tym mogą pojawić się: pogoda, RSSy, tapety pobierane co jakiś czas z Binga i inne.

 *Windows Phone 8*  dodaje Glance Screen, gdzie można wyświetlać tapety, powiadomienia, pogodę i inne na zablokowanym, wyłączonym ekranie.



### 17.	Brak możliwości przesyłania dźwięku do większości systemów audio w samochodach. Brak obsługi Bluetooth rSAP

Brak.



### 18.	Brak możliwości przesyłania dźwięku z filmów video do innych urządzeń przy pomocy bluetooth. Brak obsługi bluetooth A2DP.

Windows Phone wspiera A2DP ([Profile Bluetooth obsługiwane przez telefon Windows Phone](http://support.microsoft.com/kb/2449475)).


### 19.	Brak możliwości zaszyfrowania systemu plików. Jeżeli ktoś Ci ukradnie telefon to ma pełen dostęp do twoich plików!


Chyba na Androidzie ;) To na Andku wszystko jest jak na tacy (usb storage mode, oł yeah :P )  W WP aplikacje działają w izolowanym środowisku i nie współdzielą one bezpośrednio swoich plików. Co więcej system plików nie jest dostępny po podłączeniu do komputera. Jeśli doda się do tego blokadę ekranu na hasło, to wówczas nawet nie zsynchronizuje się plików poprzez Zune! Nie ma mowy o jakimś prostym dostępie do danych! Jeśli chce się więcej, w Markeplace są aplikacje do zabezpieczania plików na hasło. Nieźle co? ;)

Ale to jeszcze nie wszystko. Otóż Windows Phone, w razie zgubienia urządzenia oferuje z poziomu www: zablokowanie urządzenia, wymazanie danych, lokalizację telefonu, włączenie głośnego dzwonka, wyświetlenie komunikatu ([Odnajdywanie utraconego telefonu](http://www.microsoft.com/windowsphone/pl-PL/howto/wp7/basics/find-a-lost-phone.aspx)). I jak? ;)



### 20.	Brak możliwości korzystania z klawiatury Bluetooth
21.	Brak możliwości korzystania z klawiatury USB

Tak i myszki też nie podłączy się do Windows Phone :)



### 22.	Bardzo niewiele możliwości dostosowania telefonu do pod siebie.

Mając jednak odblokowany telefon można zdziałać cuda. A standardowo jest skromnie, ale stylowo ;)

 *Windows Phone 7.8* 

Dodano 3 rozmiary kafelków oraz nowy ekran blokady, który pobiera tapety bezpośrednio z BInga, nowe kolory motywów.

 *Windows Phone 8* 

Dodano 3 rozmiary kafelków, nowy ekran blokady, który pobiera tapety bezpośrednio z BInga,  nowe kolory motywów, każda aplikacja może wrzucać własne elementy na ekran blokady, wiele zmian w UI.


### 23.	Prawdopodobnie nie będzie możliwości zaktualizowania do WP8. (plotki w różnych serwisach technologicznych)


O tak, dobrze, że ktoś ma 100% informacje. Nikt nie wie jeszcze jak to będzie, ale wszystko wskazuje na to, że jednak będzie aktualizacja. No cóż ;)

 *Windows Phone 7.8* 

Dla systemu z linii 7.x przygotowano aktualizację 7.8.


### 24.	Pasek z stanem baterii, siłą sygnału, nazwą operatora itp nie jest stale widoczny.

To jest świetny pomysł i szybko można się przyzwyczaić i zrozumieć "filozofię". Stan błyskawicznie sprawdza się, poprzez delikatne przeciągnięcie palcem po górnej krawędzi ekranu. Co więcej, jeśli np. urządzenie łączy się poprzez WiFi, zmiana stanu jest pokazywana na pasku, podobnie np. gdy jest słaba bateria. Raz użyjesz i nie będziesz chciał niczego innego ;) :P

 *Windows Phone 8.1*  - ukryty :)


### 25.	Brak możliwości zamknięcia aplikacji innego niż naciśnięcia przycisku „HOME” który przenosi nas na sam początek do 1 ekranu.

Ohh, ktoś tu chyba ze zdjęć zna WP ;) Przyciskiem "Home" (rozumiem, że chodzi o "Windows") aplikacje nie są zamykane, ale zostają uśpione w tle. Zamyka się je poprzez przycisk "Wstecz".

 *Windows Phone 8.1*  - można przeciągnąć palcem w dół i zamknąć tak apkę (w menadżerze zadań).


### 26.	Bardzo małe czcionki w wiadomościach (czcionek nie można zmieniać) są bardzo trudne do przeczytania dla starszych osób.

Wcale nie są małe, skoro dużo osób narzeka, że są za duże... ;)

 *Windows Phone 8* 

Dodano możliwość zmiany rozmiaru czcionki.


### 27.	Brak możliwości tworzenia i zapisywania playlist na telefonie.

A jednak można! Na telefonie (poprzez Zune można - to chyba oczywiste) jest możliwość stworzenia playlisty, opis: [Tworzenie listy odtwarzania](http://www.microsoft.com/windowsphone/pl-pl/howto/wp7/music/create-a-playlist.aspx).




### 28.	Brak możliwości przeszukiwania twojej kolekcji muzyki na telefonie.

Jest za to, na liście wykonawców/albumów/utworów, możliwość przejścia do piosenek poprzez litery alfabetu (jak na liście aplikacji).




### 29.	Playlista nie może być edytowane w trakcie odtwarzania.

Można patrzy wyżej.


### 30.	Brak możliwości wyłączenia odtwarzacza muzyki, możesz tylko zapauzować. Odtwarzacz muzyki pozostanie na ekranie blokowania aż do uruchomienia ponownie telefonu. Trzeba bardzo uważać, żeby przypadkiem nie włączyć muzyki np podczas spotkania. (telefon biznesowy?)

Dość mocne powiązanie z Zune daje o sobie znać. Faktycznie może być to przeszkadzać i dlatego powstałą mała apka [Stop the Music!](http://www.windowsphone.com/en-US/apps/0899997d-c25a-4075-9b28-685308e1568b) i po problemie ;)



### 31.	Brak możliwości przewijania filmów czy piosenek poprzez naciśnięcie na odpowiednie miejsce na pasku postępu.

W Zune tak. Jednakże, przyciski do przewijania działają jak trzeba.




### 32.	Kontakty online i offline są pomieszane ze sobą. Brak jakiejkolwiek możliwości do filtrowania!

"wiadomości" (przewiń poziomo) "dostępni" - lista dostępnych :) Czy może być prościej?




### 33.	Brak możliwości zapisania kopii roboczych smsów!

Nie ma, ale czy naprawdę ktoś tego używa? :P




### 34.	Przycisk wyszukiwania przy wybieraniu numeru nie wyszukuje numerów do wybrania ale przeszukuje historię ostatnich połączeń.

Może temu, że jest się w oknie "historia", a nie "kontakty"? :P



### 35.	Wiadomości mogą być tylko usuwane jedna po jednej albo cały wątek.

Dokładnie tak jest.

 *Windows Phone 8* 

Można usuwać całość lub pojedynczo albo po całym wątku.


### 36.	Brak możliwości wybrania kilku zdjęc do usunięcia , wysłania albo zuploadowania. Muszą być dodawane jedna po jednej.

Dokładnie tak jest (chyba, że usuwa się cały album).

 *Windows Phone 8* 

Funkcja została dodana.


### 37.	Brak jakichkolwiek szczegółów na temat zdjęć takich jak data czy czas zrobienia, rozmiar.

Zdjęcia przeglądać można m.in. w menu, gdzie są one porozmieszczane wg. konkretnych dat stworzenia. Istnieje w Marketplace aplikacja [Photo Info](http://www.windowsphone.com/pl-PL/apps/75c1d064-e221-e011-854c-00237de2db9e), która wyciąga ze zdjęcia wszelkie informacje. 


### 38.	Programy są zawsze pogrupowane alfabetycznie. Brak możliwości grupowania np po kategorii.

Taka opcja jest najbardziej intuicyjna, ale po odblokowaniu telefonu, można grupować w foldery poprzez aplikację [Folders](http://windowsphonehacker.com/folders).




### 39.	Kalendarz nie ma trybu do pokazywania tygodnia i widok miesięczny nie można zoomować.

 *Windows Phone 8.1*  kalendarz przeszedł metamorfozę i dodano wiele ciekawych i nowych opcji.


### 40.	Brak live wallpapers.

Dokładnie tak jest.

 *Windows Phone 7.8* 

Tapety Bing (pobierane automatycznie).

 *Windows Phone 8* 

Jest coś zupełnie innego, a mianowicie tapety Bing (pobierane automatycznie) i możliwość instalacji aplikacji przeznaczonych do podmiany treści na ekranie blokady.


### 41.	Brak jakichkolwiek innych klawiatur (takich jak Swype, nie wyobrażam sobie pisania bez tego)

 *Windows Phone 8.1*  - jest Swype!



### 42.	Brak obsługi flashplayera

Po co? Jest obsługa HTML5!


### 43.	Brak obsługi programów napisanych w javie

Pffff :D A na Androidzie nie ma natywnego .NETa ;)


### 44.	Brak możliwości tworzenia screenshotów!

Po odblokowaniu: [Screen Capturer](http://forum.xda-developers.com/showthread.php?t=1316199).

 *Windows Phone 8* 

Już jest.


### 45.	Brak możliwości automatycznego zmieniania tapet

Po odblokowaniu: [Lock Widgets](http://windowsphonehacker.com/articles/lock_widgets_official_release-03-28-12)  m.in. tapety pobierane z Binga, pogoda, RSSy i inne.

 *Windows Phone 7.8* 

Dodano tapety z Binga.

 *Windows Phone 8* 

Już jest (tapety Bing), a nawet więcej (aplikacje do wrzucania własnego contentu na ekran)!


### 46.	Brak możliwości interakcji ze sprzętem przez programistów. Przez to wiele ciekawych programów nigdy nie powstanie.

Kwestia czasu, [WP7 Root Tools SDK](http://wp7roottools.com/) się rozkręca ;)

 *Windows Phone 8* 

Dodanie tworzenia aplikacji w C++, czy DirectX.



### 47.	Brak equalizera dla odtwarzacza muzyki Zune.

Zgadza się.

 *Windows Phone 8* 

Jest np. w Nokiach.


### 48.	Brak możliwości zliczania ilości pobranych danych pakietowych

Nokia posiada aplikację Nokia Counters (Nokia liczniki), która tym się zajmuje.

 *Windows Phone 8* 

Dodano aplikację Data Sense to liczenia danych pakietowych.


### 49.	Internet Explorer nie ma możliwości pobierania plików czy przeglądania stron w trybie offline

Na szybkiego znalazłem [Offline Browser](http://www.windowsphone.com/pl-PL/apps/e34e28aa-b6bc-48f5-b3f8-62f0dc41757f), pewnie coś darmowego też jest.



### 50.	Brak jakichkolwiek innych przeglądarek niż Internet Explorer!

Nie oszukujmy się, mobilna wersja IE jest świetna! Czego jej brakuje? :) 
Jest ich bardzo wiele: Nokia Xpress, UC Broswer i inne.



### 51.	Przyciski przyciszania/podgłośniania nie mogą być używane do zoomowania przy robieniu zdjęć.

Yyyy? A dlaczego miałoby to tak działać?


### 52.	Nie można otworzyć plików zip czy rar wysłanych jako załącznik maila.

Windows Phone wspiera w pełni spakowane pliki ZIP.


### 53.	Nie można wysyłać czy otwierać filmów video wysłanych przez MMS.

Można już, jak najbardziej.

### 54.	OfficeMobile ma znacznie mniej możliwości niż zewnętrzne programy takie jak SMartOffice, QuickOffice czy Polaris. Wstyd.

I jeszcze mniej niż desktopowy Office :) Mobilny Office spełnia swoje zadanie: edycja dokumentów. Nikt nie będzie pisał pracy mgr w nim :)


### 55.	Czas wysłania emaila nie uwzględnia roku.

W formacie daty nie wyświetla (aby było więcej miejsca przypuszczam), ale uwzględnia rok. 


### 56.	Różne aplikacje są dostępne dla różnych krajów.

Taka polityka. Developer wrzuca aplikację, tam gdzie chce. Jeśli ktoś nie chce by była  ona ściągana poza jakimiś regionami, to cóż na to poradzimy? Nie ma ich jednak dużo.


### 57.	Nie wszystkie możliwości są dostępne dla osób spoza USA.

Rozumiem, że np. Bing. Co ciekawe, żeby mieć dostęp do tych rzeczy nie trzeba zmieniać języka telefonu. Wystarczy mienić język wyszukiwarki. Tylko tyle!


### 58.	Jedna możliwość kontroli głośności dla dzwonków, powiadomień czy alarmów.

Dokładnie. Ma to swoje plusy i minusy.

 *Windows Phone 8.1*  - zmieniono. System i multimedia mają oddzielne paski głośności  :)


### 59.	Wifi rozłącza nas z internetem kiedy ekran się wyłącza.  Po wyłączeniu ekranu twój telefon zaczyna korzystać z 3G!

Poważnie?! :P Rozłączenie z WiFi, gdy ekran jest wyłączony jest spowodowane oszczędzaniem baterii. Inaczej można byłoby rozładować słuchawkę bardzo szybko. W WP wiemy co się dzieje. Nie ma możliwości, że w tle, bez wiedzy użytkownika coś się ściągnie. Co do 3G, jeśli jest włączone 3G to przejdzie na 3G, ale można 3G normalnie wyłączyć (szok! :P ).

Jednakże w Marketplace dostępna jest malutka aplikacja [Keep Alive](http://www.windowsphone.com/pl-pl/store/app/keep-alive/a4c10936-c5a5-42d7-af4c-1453ca7cf951), która, gdy działa w tle, podtrzymuje wifi nawet po wyłączeniu ekranu.

 *Windows Phone 8* 

Aktualizacja Portico wprowadza pobieranie danych przez WiFi przy wygaszonym ekranie. 


### 60.	Możesz wpisać tylko 1 numer telefonu komórkowego dla każdego kontaktu.

Tak jest. Ale tu chodzi tylko o typ. Jeśli ktoś zechce, to do jednego kontaktu dodaje ile zapragnie nr. Można traktować to jako nr główny (np. do wysyłania smsów). 


### 61.	Nie możesz wysyłać MMSów bez włączonego internetu.

MMSy wysyłane są poprzez 3G.


### 62.	Telefony nie mogą być ładowane kiedy wyłączone.

Jeśli zaczniemy ładować wyłączony telefon, wówczas (jeśli pozwala na to bateria) zostaje on uruchomiony. Chyba tak to powinno działać? :)


### 63.	Telefon musi być podłączony do ładowarki, żeby móc go synchronizować bezprzewodowo. To mnie najbardziej śmieszy. Microsoft ma inną definicję słowa bezprzewodowo.

Opcja automatycznej, bezprzewodowej (bez podłączenia urządzenia do komputera) synchronizacji zostaje uruchomiona, gdy tylko podłączy się urządzenie do ładowania na dłużej niż 10 min. To jest w 100% idioto odporne. Robi się to automatycznie, ale dzięki temu wymogowi, gdy zapomni się o synchronizacji, nie będzie niemiłego zaskoczenia, "że w domu telefon trzyma krócej".



### 64.	Ogromne czcionki w niektórych miejscach marnują tylko przestrzeń.

A wcześniej, że czcionka za mała? :) Nie dogodzisz wszystkim ;)


### 65.	Brak możliwości przesyłania plików przy pomocy bluetooth.

Jak ludzie bez tego, żyją?! :P

 *Windows Phone 7.8* 

Lumie mogą już wysyłać/obierać pliki przez BT.

 *Windows Phone 8* 

Taka opcja jest już w standardzie.


### 66.	Brak możliwości rozdzielenia historii połączeń na połączenia nieodebrane, odebrane, wybrane, ostatnie itp.

Nieodebrane wydzielone są innym kolorem, reszta ma stosowny opis. 


### 67.	Nie pokazuje czasu połączenia w ostatnich połączeniach.

Faktycznie, nie zauważyłem tego. Widocznie, można funkcjonować bez tego.

 *Windows Phone 8.1*  - pokazuje :)


### 68.	Nie możemy backupować ani SMSów ani historii połączeń.

Po odblokowaniu: [SMSBackup](http://forum.xda-developers.com/showthread.php?t=1448197).

 *Windows Phone 8* 

Można robić backup na SkyDrive.


### 69.	Nie można wysyłać kontaktów jako wizytówki csv.

Wizytówki nie działały u mnie, czasem nawet pomiędzy dwoma Nokiami :P Zarządzać zaś kontaktami można poprzez konto @live.com, gdzie siedzą wszystkie dane.


### 70.	Brak możliwości wyświetlania długich nazw w nazwach piosenek lub filmów (są ucinane!).

Ale są za to duże :P


### 71.	System nie zmiejsza głośności powiadomień przy słuchaniu muzyki na słuchawkach. Niekiedy przychodzący SMS może nam rozwalić bębenki.

A kto tak głośno słucha muzyki? :) Ale faktycznie to powinno być jakoś zmieniane.


### 72.	Brak obsługi Silverlight.

To tak jak z Flashem. Jest HTML5, czego chcieć więcej? :)


### 73.	Wbudowane zdjęcia w emaile nie pobierają się.

Yhh. Jak to się nie widziało nigdy WP i przetacza się czyjeś opinie to tak bywa. W Windows Phone rozwiązane jest to wzorowo. Ze względu na to, żeby nikt nie narzekał, że maile same ściągają "wbudowane" duże zdjęcia, nie są one automatycznie pobierane. Jeśli ktoś jednak chce pobrać załączone w kodzie HTML zdjęcia (najczęściej jest tak w reklamach!), wystarczy dotknąć link na dole maila: "Pobierz wiadomość i zdjęcia z Internetu (około: podany_rozmair_do_ściągnięcia)". Świetne, czyż nie? :)


### 74.	Brak możliwości przeglądania stron przy pomocy proxy.

Podłączając się do sieci jest możliwość wyboru proxy. Więc problem z głowy. Co więcej, każdy kto chce pracować w trybie incognito, może ściągnąć np. darmową przeglądarkę [UC Browser](http://www.windowsphone.com/en-US/apps/057a2909-2e93-e011-986b-78e7d1fa76f8).

 *Windows Phone 8*  - dodano proxy do WiFi


### 75.	Brak możliwości korzystania z sieci Tora.

Może ktoś przeportuje Tora na WP. Tylko, ile ludzi z tego korzysta na urządzeniach mobilnych?





### 
[AKTUALIZACJA]
Zmiany po Microsoft Windows Phone Summit
 

Nie chcę by zaginęło to wśród odpowiedzi. Oto co się zmieniło w poszczególnych punktach po  Microsoft Windows Phone Summit:



### 1.	Brak prawdziwego multitaskingu. Po wyjściu z programu jest on wyłączany. Najbardziej okrutnie to widać w przypadku różnego rodzaju komunikatorów.


W nowym Windows Phone 8 ma być poprawiony multitasking. Każda aplikacja będzie mogła działać w tle. Na prezentacji pokazano nowe funkcjonalności jakie dostępne będą w API dla procesów działających w tle: VoIP i geolokalizacja.



### 2.	Brak trybu pamięci masowej. Sorry.
3.	Brak obsługi kart pamięci. W ten sposób też nie prześlesz plików.

WP8 ma wspierać karty rozszerzeń microSD.


### 6.	W tej chwili jest ograniczony do właściwie jednej rozdzielczości.

Rozdzielczości wpierane przez WP8: WVGA (480 x 800), WXGA (1280 x 768) i 720p (1280 x 720).



### 19.	Brak możliwości zaszyfrowania systemu plików. Jeżeli ktoś Ci ukradnie telefon to ma pełen dostęp do twoich plików!

W nowej wersji mobilnych okienek będzie dostępne: szyfrowanie danych (Bitlocker),  secure boot, dostęp do systemu mobilnego z poziomu desktopu.




### 20.	Brak możliwości korzystania z klawiatury Bluetooth
21.	Brak możliwości korzystania z klawiatury USB

Nowe zmiany i większa integracja z Win8/RT, zapewne spowodują szersze wsparcie dla urządzeń podłączach przez BT.


### 23.	Prawdopodobnie nie będzie możliwości zaktualizowania do WP8. (plotki w różnych serwisach technologicznych)

Już wiemy, że urządzenia z WP 7.5 otrzymają wersję "legacy" 7.8. Na 7.8 nie uruchomimy aplikacja pisanych tylko dla WP8, zaś WP8 wspierać ma aplikacje z linii 7.x. Aktualizacja do 7.8 ma być dostępna dla wszystkich urządzeń z 7.5, bez względu na operatora. Więcej szczegółów zapewne poznamy  wkrótce.



### 46.	Brak możliwości interakcji ze sprzętem przez programistów. Przez to wiele ciekawych programów nigdy nie powstanie.

Na Windows Phone 8 możliwe będzie pisanie aplikacji m.in. w natywnym kodzie C/C++. Szykuje się pełne wsparcie DirectX, silników fizycznych i innych.



### 65.	Brak możliwości przesyłania plików przy pomocy bluetooth.

Najprawdopodobniej pod naciskami Nokii, zostanie to w jakimś stopniu wprowadzone w WP8.



### 69.	Nie można wysyłać kontaktów jako wizytówki csv.

Na dzień dzisiejszy Nokia, dla swoich aktualnych urządzeń oferować będzie Contact Share: "Wysyłaj i odbieraj wizytówki za pośrednictwem wiadomości tekstowych."


Oczywiście to nie wszystkie zmiany, a jedynie to co zmieniło się w odpowiedziach do poszczególnych punktów po prezentacji.

 W skrócie przedstawione zmiany na konferencji:


  * wsparcie dla procesorów wielordzeniowych



  * rozdzielczości ekranów: WVGA (480 x 800) obecna , WXGA (1280 x 768) i 720p (1280 x 720).




  * wsparcie dla kart microSD



  * nowy  Internet Explorer 10 + filtr antyphishingowy



  * wsparcie dla C/C++.



  * NFC + Wallet Hub


  * głęboka integracja ze Skypem




  * szyfrowanie (Bitlocker) i  secure boot




  * Nokia Maps dla wszystkich urządzeń z WP8




  * nowy ekran startowy




  * każdy WP z 18 miesiącami wsparcia


  * więcej funkcji biznesowych




  * WP7.5 aktualizowany tylko do wersji WP7.8




  * ulepszony multitasking

 

