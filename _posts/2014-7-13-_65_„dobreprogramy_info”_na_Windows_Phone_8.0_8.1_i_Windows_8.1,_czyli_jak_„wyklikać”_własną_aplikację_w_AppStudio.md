---
layout:     post
title:      „dobreprogramy info” na Windows Phone 8.0/8.1 i Windows 8.1, czyli jak „wyklikać” własną aplikację w AppStudio
date:       2014-07-13 15:06:00
summary:    Tworzenie aplikacji nie jest wiedzą tajemną, ale nie jest łatwo bez przygotowania stworzyć coś, co nie będzie wstyd pokazać nie tylko naszym znajomym. Jeśli chcecie dowiedzieć się jak tworzyć proste aplikacje na Windows Phone i Windows Modern, bez dotykania do kodowania, to zapraszam do wpisu.Tekst, który czytacie kierowany jest zarówno do osób nie mających nic wspólnego z programowaniem oraz do t...
categories: oprogramowanie programowanie urządzenia mobilne
---



Tworzenie aplikacji nie jest wiedzą tajemną, ale nie jest łatwo bez przygotowania stworzyć coś, co nie będzie wstyd pokazać nie tylko naszym znajomym. Jeśli chcecie dowiedzieć się jak tworzyć proste aplikacje na Windows Phone i Windows Modern, bez dotykania do kodowania, to zapraszam do wpisu.

Tekst, który czytacie kierowany jest zarówno do osób nie mających nic wspólnego z programowaniem oraz do tych, którzy już mają pewną praktykę w tworzeniu aplikacji. Ci pierwsi będą mogli stworzyć proste programy na  smartfony czy tablet bez dotykania do kodowania, drudzy zaś mogą chociażby podejrzeć kod wynikowy tak stworzonych aplikacji w celu nauki. 

Poniższy tekst bazuje na prezentacji przygotowanej na tegoroczny [HotZlot](http://www.hotzlot.pl/).

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140713144157_0.jpg)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140713144002_0.jpg)


Stworzona w opisywany sposób aplikacja została opublikowana w markecie Windows i Windows Phone.

Zaczynamy!


## AppStudio - podstawy

Nasze aplikacje tworzyć będziemy w AppStudio, narzędziu dostarczonym przez Microsoft. Co ważne, nie musimy nic instalować, ani pobierać z sieci. Narzędzie te obsługuje się z poziomu przeglądarki internetowej. Do stworzenia tego poradnika użyłem aktualnej wersji Chrome, ale spokojnie można wykorzystać Firefoxa czy nowsze wersje Internet Explorera.

AppStudio jest narzędziem do tworzenia aplikacji  *kafelkowych*  na Windows Phone 8 i 8.1 oraz na Windows 8.1. Raz wyklinany program, będzie działał jednocześnie na obu tych systemach. Wystarczy zatem wejść na stronę [AppStudio](http://appstudio.windows.com/) i zalogować się kontem live. Nie ma żadnych ukrytych kosztów czy rozbudowanych formularzy rejestracyjnych. Wejście w świat AppStudio jest naprawdę proste i przyjemne.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161927_0.png)

Aplikacje tworzone w AppStudio są proste i można traktować je jako wizytówki, oprogramowanie do prezentacji produktów czy jako agenda do różnych wydarzeń. Do budowy naszej apki wykorzystać możemy kilka przygotowanych  *scenariuszy* . Mowa tutaj o pobieraniu danych z RSS, YouTuba, Facebooka, Binga, Instagrama czy Flickra. W takim wypadku wystarczy podać link do źródła, a aplikacja sama zadba o dynamiczne ładowanie danych, stronę ze szczegółami itp. Można również dodawać statyczne informacje, tutaj źródłem danych będą wpisane przez nas informacje lub plik csv, który przyspieszy ten proces. 

Tworzenie programu sprawdza się do klikania i przenoszenie elementów w poszczególne miejsca w oknie przeglądarki. Poniższy punkt przedstawi tworzenie przykładowej aplikacji krok po kroku z omówieniem poszczególnych elementów w AppStudio.


## dobreprogramy info - aplikacja z AppStudio na Windows Phone 8/8.1 i Windows 8.1


W tym  *samouczku*  stworzymy przykładową aplikację w AppStudio. Jednakże, aby nie marnować czasu, nasza aplikacja wynikowa będzie źródłem informacji o portalu dobreprogramy, czyli coś czego nie ma jeszcze na Windows Phone (portal wydał jedynie wersję pod Windows). Będzie ona zawierała dynamicznie ładowane dane z RSS oraz Facebooka i YouTuba. Do dzieła!


### Start


Tuż po zarejestrowaniu się, ujrzymy ekran z projektami. Z racji tego, że jest to nasz pierwszy kontakt z tym portalem, okno będzie jeszcze puste:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161934_0.png)


Po kliknięciu na  *Start new project*  zostaniemy przeniesieni do wyboru szablonu naszej przyszłej aplikacji:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161936_0.png)


Możemy w tym miejscu zdecydować się czy zechcemy stworzyć nową aplikację na bazie istniejącego już szablonu lub samemu zaprojektować ją od nowa. Wybierzemy w tym przypadku pustą aplikację, aby móc samemu zaprojektować wynikowe oprogramowanie. 


AppStudio przypomni nam jeszcze, że stworzona tak aplikacja działać będzie zarówno pod Windows Phone, jak na urządzeniach z Windows 8.1:

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161938_0.png)



### Podstawy


Klikamy na  *Create* , a wówczas zostaniemy przeniesieni do głównego okna AppStudio:

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161940_0.png)

Tutaj zauważymy, że aplikacje stworzone w tym narzędziu opierają się o tzw.  *panoramę* . Jest to rodzaj kontrolki, który pozwala na przewijanie ekranów z danymi (takich ekranów możemy dodać maksymalnie 6). Każdy z ekranów może posiadać element, który będzie jednego  *typu* . Może być to Facebook, RSS, lub inne dane ładowane dynamiczne, ewentualnie można wstawić własny kod HTML. Dodatkowo z sekcji  *advanced*  można wybrać zaawansowane elementy jak listy i kolekcje danych idealne do prezentacji informacji. My skorzystamy tylko z zaznaczonych pozycji, które będziemy dodawać w puste pola. 

Na górze zaznaczyłem miejsce, gdzie można dodać nazwę aplikacji i ikonę (tekst i grafika przewijać się będą wraz z przewijaniem ekranów). Wpiszmy zatem nazwę aplikacji dobreprogramy info oraz wybierzmy ikonę z naszego dysku (warto by miała ona przezroczyste tło):


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161943_0.png)


Teraz będziemy dodawać poszczególne elementy do głównego okna. Pamiętajmy, aby po każdej zmianie w poszczególnym oknie zapisywać postęp prac przyciskiem  *Save* .




### RSS, YouTube, Facebook, HTML - konfiguracja
 

Mamy już przygotowane okno, teraz umieśćmy na nim poszczególne elementy. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161944_0.png)

Zaczniemy od RSSów. Klikamy na odpowiednią ikonę, a wówczas ukaże się nam konfiguracja tej sekcji. Dodajmy teraz nagłówek i źródło danych, w postaci linka do RSSów.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161947_0.png)


Zróbmy podobnie z YouTubem. Tutaj źródłem danych jest nazwa profilu na portalu.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161948_0.png)


Konfiguracja Facebooka wygląda identycznie, jak w przypadku YouTube.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161949_0.png)


Mamy już okno z trzema sekcjami. Jeśli kolejność nas nie satysfakcjonuje, możemy ją zmienić przenosząc ikony. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161950_0.png)

Dodajmy jeszcze element HTML i tam wpiszemy krótką notkę o autorze aplikacji.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161952_0.png)


Stworzyliśmy zatem podstawowe elementy naszej aplikacji. Możemy na podglądzie przewijać już okno, a nawet zobaczyć jak będzie to wyglądało na Windows 8.1 (tablet), poprzez kliknięcie w zielony przycisk  *Windows Preview* .



### RSS, YouTube, Facebook - doprecyzowanie szczegółów


Nasza aplikacja posiada już całkiem znośny wygląd, czas teraz na dopieszczenie szczegółów. Klikając na przycisk  *Edit*  możemy skonfigurować poszczególne sekcje. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161953_0.png)


Na początek zajmiemy się RSSami. Zmienimy layout na bardziej przejrzysty. Wystarczy kliknąć na wybrany typ, a podgląd odświeży się automatycznie i przedstawi nam wybrany schemat.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161958_0.png)


Teraz wejdźmy na szczegóły RSSów (ikona na prawo). Okno te będzie pojawiać się, po kliknięciu na element na liście. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712161959_0.png)

Zmienimy tutaj sposób prezentacji okna. Możemy w tym miejscu ustalić jakie dane mają pojawiać się w poszczególnych miejscach szczegółów z RSS.




Zapiszmy zmiany i przejdźmy do kolejnych szczegółów w głównych elementach aplikacji. W oknie YouTuba zmienię wygląd, aby był on bardziej podobny do tego co zostało ustawione w RSSach.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162002_0.png)

W przypadku Facebooka zmienimy więcej w prezentacji danych. W tym miejscu zdjęcia nie zawsze są wrzucane do profilu, stąd też zarówno główne okno, jak i szczegóły, będą opierały się tylko na danych tekstowych.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162005_0.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162007_0.png)


Po zapisie nasza aplikacja wygląda w następująco:

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162010_0.png)



### Style

Przejdźmy na zakładkę  *Themes* , aby zmienić styl naszej aplikacji.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162013_0.png)

W tym miejscu możemy zabawić się kolorami, aczkolwiek warto pamiętać o umiarze. Stworzona aplikacja musi być czytelna zarówno w jasnym, jak i ciemnym stylu. Ja zostawiłem tutaj wartości domyślne, a dodałem jedynie tło, które będzie przesuwać się, wraz z przewijaniem ekranu.

Warto w tym miejscu jeszcze sprawdzić, jak będzie prezentować się aplikacja na Windows 8.1, poprzez kliknięcie na zielony przycisk Windows Preview

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162025_0.png)



### Kafelki oraz ekran startowy i blokady

Przejdźmy do trzeciej zakładki  *Tiles* . To w niej zdecydujemy jak mają wyglądać i zachowywać się kafelki przypięte do ekranu startowego oraz ikona aplikacji.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162027_0.png)

Można tutaj wybrać jeden z trzech sposobów prezentacji kafli. Pierwszym z nich jest dwustronny kafelek. Po jednej stronie mamy grafikę, po drugiej tekst. Drugi sposób to kafelki, na których przewijane są (w sposób cykliczny) grafiki. Trzecim typem jest statyczny kafelek, którego dane zmieniają się w zależności od wybranego rozmiaru.

Wybrałem ostatni schemat i umieściłem w nim odpowiedni tekst i grafikę.

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162032_0.png)

Niestety, w obecnej wersji AppStudio, najszerszy kafelek w tym szablonie nie wyświetla się poprawnie na maszynie docelowej (grafika jest niepotrzebnie rozciągana na całą szerokość kafla).

Dodatkowo po przejściu do  *Splash&Lock*  skonfigurujemy ekran startowy na Windows Phone i Windows oraz ekran blokady na Windows Phone. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162035_0.png)

Warto pamiętać, że podgląd nie zawsze pokazuje wynikowy efekt, jaki będzie dostępny na urządzeniu. Otóż w aplikacji grafika jest rozciągana na cały ekran, co nie jest pokazane na podglądzie. Stąd też ekran startowy i blokady na Windows Phone warto przygotować w rozdzielczości 720p, wówczas będziemy mieli pewność, że obraz się nie rozjedzie i będzie wyglądał poprawnie na każdej rozdzielczości urządzenia.

Na tym etapie naszą aplikację można uznać za skończoną, czas teraz na ostatni element, czyli publikację.


### Przygotowanie do publikacji

Ostatnia zakładka przedstawia nam końcowy efekt naszej pracy. To tutaj przygotowujemy opis i poszczególne elementy niezbędny przy publikacji jej do marketu. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162041_0.png)

Dodajemy tutaj opis i nazwę naszej apki, a także, jeśli tego sobie życzymy, umieszczamy reklamy. Jeśli posiadamy konto deweloperskie, w opcji * Associate App with the Store,*  łączymy wynik pracy z kontem w sklepie, co pozwoli później na dodanie tak stworzonego programu do marketu Windows Phone i Windows.

Po ustawieniu opcji wg naszych upodobań, możemy kliknąć na przycisk  *Finish* . W tym momencie podgląd naszej aplikacji zostanie jeszcze raz pokazana na Windows Phone i Windows. Klikamy na  *Generate,*  aby wygenerować pliki wynikowe. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162057_0.png)


W otwartym oknie możemy wybrać typ docelowego pliku. Może być to aplikacja Universal App, którą zainstalujemy zarówno na Windows Phone 8.1 oraz Windows 8.1 (tylko te dwie wersje wspierają Universal Apps) lub program przeznaczony tylko na Windows Phone 8.0. Oczywiście jeśli chcemy stworzyć aplikację na te trzy systemy, musimy generowanie uruchomić dwa razy. 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140713140939_0.png)

W tym miejscu zdecydujemy również o tym, czy AppStudio ma stworzyć gotowy plik przygotowany do wrzucenia do sklepu (AppStudio samo zrobi screeny ekranów, aby wrzucić je do marketu!) oraz do instalacji bezpośrednio na urządzenie.

Wygenerowane dane będą zawierały wybrane opcje oraz stworzone w ten sposób źródła aplikacji do pobrania w formie pełnej solucji pod Visual Studio 2013.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140712162104_0.png)


To w zasadzie tyle. Teraz możemy przejrzeć kod w celu nauki, umieścić aplikacje w markecie (jeśli mammy konto deweloperskie) lub zainstalować apkę na urządzeniu ([opis jak to zrobić](http://appstudio.windows.com/Home/HowTo#device)). 


## Pobierajcie i testujcie

Wynikowe aplikacje umieściłem w markecie Windows Phone 8.0/8.1 oraz Windows 8.1. Możecie przetestować i sprawdzić jak działa oprogramowanie stworzone całkowicie za pomocą AppStudio:

dobreprogramy info - [Windows Phone 8.0/8.1](http://www.windowsphone.com/pl-pl/store/app/dobreprogramy-info/90c16da1-5d50-411e-840e-c57a097712a4), do pobrania także z [bazy aplikacji](http://www.dobreprogramy.pl/dobreprogramy-info,Program,WindowsPhone,58591.html) portalu dobreprogramy

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140713142259_0.png)


dobreprogramy info - [Windows 8.1](http://apps.microsoft.com/windows/pl-pl/app/dobreprogramy-info/1e033ea7-422b-41e9-863f-b2bf6f10cd8b)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-7-13-_65_/g_-_608x405_-_-_56374x20140713142302_0.png)



## Uwagi i porady

Mam nadzieję, że opis okaże się pomocny. Szybko można stworzyć własną, prostą aplikację, bez znajomości programowania. Na koniec dodaję kilka uwag odnośnie samego AppStudio, jak i kilka ogólnych porad: 




  * szczegółowy, bardzo dobry opis AppStudio znajdziemy na [oficjalnej stronie](http://appstudio.windows.com/Home/HowTo)


  * wynikowa aplikacja obecnie jest tworzona tylko w języku angielskim


  * przejście do strony www z RSS/FB/YT wymaga w Windows Phone kliknięcia na [...] i wybrania opcji  *go to source* , w Windows 8.1 należy kliknąć prawym klawiszem, aby ukazało się menu - jest to mało intuicyjne, lepiej aby przejście do źródłowych stron odbywało się poprzez kliknięcie w nagłówek lub tekst


  * AppStudio ma problem z generowaniem szerokich kafli, przypinanych do strony startowej


  * AppStudio nie generuje przezroczystych ikon aplikacji, mimo załadowania grafik png z przezroczystością 


  * wynikowe screeny z aplikacji pod Windows 8.1 są o 2 piksele za duże! :P aby wrzucić te grafiki do marketu (oczywiście można zrobić to ręcznie, ale jest to ewidentne niedopatrzenie)


  * Microsoft udostępnia [przykładowe aplikacje](http://appstudio.windows.com/Home/SampleApps) na Windows Phone 8.1 i Windows 8.1, które prezentują możliwości AppStudio


  * brakuje możliwości wygenerowania wyników pod Androida czy iOS, dodanie tej opcji nie wydaje się być problematyczne, a uatrakcyjniłoby AppStudio


  * brak wsparcia Twittera 


  * brak wsparcia dla bardziej zaawansowanych źródeł danych jak np. WebService


  * brak konfiguracji paska menu


  * wynikowe aplikacje mogą być użyte do celów komercyjnych


  * dodanie aplikacji do marketu wymaga posiadania płatnego konta deweloperskiego  


  * nie liczmy na  *miliony*  z reklam w tego typu apkach :) 



