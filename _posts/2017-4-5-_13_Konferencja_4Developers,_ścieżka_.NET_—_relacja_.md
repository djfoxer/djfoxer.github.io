---
layout:     post
title:      Konferencja 4Developers, ścieżka .NET — relacja 
date:       2017-04-05 18:13:00
summary:    W dniu 3 kwietnia uczestniczyłem w imprezie 4Developers w Warszawie. Organizatorzy określają event jako interdyscyplinarny festiwal technologiczny dla programistów, czyli konferencja dla programistów z wieloma ścieżkami do wyboru. W tym roku było na prawdę zacnie. Oto moja krótka relacja z tego even...
categories: porady programowanie inne
---



W dniu 3 kwietnia uczestniczyłem w imprezie [4Developers](http://2017.4developers.org.pl/pl/) w Warszawie. Organizatorzy określają event jako  *interdyscyplinarny festiwal technologiczny dla programistów* , czyli konferencja dla programistów z wieloma ścieżkami do wyboru. W tym roku było na prawdę zacnie. Oto moja krótka relacja z tego eventu.






![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211015_0.png





## Co, gdzie, jak i kiedy?


[4Developers](http://2017.4developers.org.pl/pl/) odbyło się w warszawskim hotelu Hotelu Sangate Airport, obok portu lotniczego im. Fryderyka Chopina. Miejscówka idealnie położona jeśli ktoś przyjeżdżał na konferencję autem (łatwy dojazd obwodówką). Z dworca PKP dojazd również nie był męczący (przejazd autobusem bez przesiadek), chociaż trzeba było przejechać przez ścisłe centrum, więc cudów nie oczekiwałem :)

Wydarzenie nie było skierowane tylko do wybranego grona deweloperów. Mieliśmy do wyboru aż 14 ścieżek:


  * App Arch I By Allegro


  * App Arch II By Decerto


  * Java


  * JavaScript By Pracuj.Pl


  * .Net I By Lingaro


  * .Net II By Sii


  * Python


  * WORKSHOPS


  * PHP


  * Ruby


  * Bottega IT Minds


  * Business Relations &amp; Soft Skills


  * GameDev


  * Front-End



W każdej z nich było 7-10 prezentacji. Daje to nam prawie 130 prezentacji w ciągu jednego dnia! Naprawdę było ciężko czasami wybrać na co iść w danej chwili. Nie było opcji, że ktoś nie mógł znaleźć czegoś dla siebie.

Pomimo, że zdecydowałem się na ścieżkę .NET to kusiły również inne tematy. Bardzo ciekawie prezentowały się także prezentacje z JavaScriptu, architektury czy luźne panele dyskusyjne.

Szkoda, że tyle interesujących prelekcji odbywało się w tym samym czasie. Widziałem jednak, iż każda prezentacja była nagrywana, zatem liczę w najbliższej przyszłości na udostępnienie nagrań.

Od strony merytorycznej (przynajmniej na prezentacjach, na których byłem) wielki plus za dobór prelegentów i tematyki. Każda z prelekcji wypadła bardzo ciekawie i nie mam się do czego przyczepić. Brawo!

Partnerzy również dopisali i główne miejsce, gdzie można było zjeść, popić i pogadać z nimi, spisywało  się rewelacyjnie. Dużo miejsca, kącik relaksu, piwko. Czegóż chcieć więcej? :)

Mógłbym tylko delikatnie ponarzekać na to że w trakcie przerw było bardzo ciasno. Prezentacje rozmieszczone były na 3 piętrach i wąskim gardłem stały klatki schodowe. gdzie ścisk był spory.

Przejdźmy jednak do samych prezentacji. Oto krótka relacja z tego co działo się na wybranych prelekcjach ze ścieżek .NET (niestety na wszystkich fizycznie nie mogłem być, co ubolewam).



## Prezentacje (wybrane ze ścieżek .NET)


W kilku krótkich zdaniach opiszę prelekcje na jakich byłem. Nie chcę tworzyć ich streszczeń, a jedynie przedstawić zagadnienia o jakich była mowa z krótką oceną na koniec.



### Functional developer in object oriented world - how F# helped me to write better C# - Bartosz Sokół



Pierwszą prezentacją była prelekcja odnośnie tworzenia kodu C# inspirowanego F#. Praktyczne podejście do tego jak uprościć czytelność kodu i jego logikę. Eliminacja ifów i sprawdzania nulli, użycie obiketów Immutable, a także tworzenie generycznych, uniwersalnych maszyn stanowych,  które pomogą w zapanowaniu nad serwisami. Co ciekawe w prezentowanych założeniach ograniczono Dependency Injection do minimum, zastępując je statycznymi  *repozytoriami* .

Ciekawy temat zarówno w przypadku, gdy chcemy zacząć przygodę z F#, jak i udoskonalić rozwiązania w C#. Warto przy okazji odwiedzić stronę [F# for fun and profit](https://fsharpforfunandprofit.com/).



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211024_0.jpg





### Make c# objective again - Karol Rogowski


W kolejnej prezentacji pokazane były główne błędy w programowaniu obiektowym (nie tylko C#), które  *spłaszczały*  OOP. Obok typowych złych nawyków pokazano, jak ominąć pułapki i upiększyć jednocześnie nasz kod.

Bardzo interesujący temat, który zainteresował wszystkich na sali. Główny przekaz to używanie faktyczne obiektywności, nie obrażanie się na extensiony, interfejsy i najważniejsze - planowanie kodu. Co nam różnie wychodzi :)



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211025_0.jpg





### ETW w służbie programisty .NET - Konrad Kokosa


Czym jest ETW? To Event Tracking for Windows, czyli potężny, ale nieznany szerzej system (silnie typowany) do logowania. Otrzymaliśmy ciekawą porcję wiedzy o tym jak logować i odczytywać logi, zarówno poprzez narzędzia systemowe, zewnętrzne, jak i w aplikacjach .NET. 

Chętni zapewne powinni przejrzeć w sieci aplikacje związane z ETW - Windows Performance Toolkit czy Perfview. Co ważne, od .NET 4.5 tworzenie logów do ETW zostało nareszcie uproszczone! Wygląda to dość ciekawe w przypadku, gdy chcemy prześledzić wycieki pamieć lub przyspieszyć działanie naszej aplikacji.



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211026_0.jpg





### .NET Core w 2017 - Łukasz Pyrzyk


Niezmiernie ciekawą prezentacją była ta przygotowana przez Łukasza Pyrzyka. Temat .NET Core budzi emocje u każdego programisty tworzącego w technologii Microsoftowej. Dowiedzieć się można było odnośnie planowanej wersji .NET Core 2.0 i .NET Standard 2.0 (wraca csproj[!], możliwość importu dllek ze starego .neta ), a także o zagrożeniach jakie wynikają z używania nowego frameworku (nie wszystko będzie działać, słaba reużywalność).

Sala pękała w szwach, temat .NET Core ściągną wiele osób i ci co przyszli na pewno się nie zawiedli. Było sporo ciekawostek (np. brak Emita z refleksji w Xbox One) i nowinek. Świetna prezentacja, a przekaz z niej jest następujący:  *Czekajcie do .NET Core 2.0*  :)



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211028_0.jpg

  

Prz okazji pozdrawiam [Łukasza Pyrzyka](https://pyrzyk.net/), u którego [na blogu wygrałem](https://pyrzyk.net/win-ticket-4developers-conference/) wejściówkę na konferencję 4Developers. Dzięki jeszcze raz! :)



### Serverless w C# -  Jakub Gutkowski


Po przerwie obiadowej przyszedł czas na kolejne prezentacje. Tym razem wybór padł na Serverless, czyli następce mikroserwisów. Było szybkie wprowadzenie do kontenerów i przedstawienie serverlessów jako czegoś... co już znamy od dawna. Czyli kolejne wcielenie usług serwerowych po hostingu i chmurze.

Były różnice pomiędzy użyciem nanoserwisów opartych o Lambda (Amazon) i Functions (Azure) i live coding. Całkiem ciekawy temat, dość mocno przyszłościowy.



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211029_0.jpg





### Nie tylko RESTful - poznaj GraphQL - Piotr Gankiewicz

  
Na kolejną prezentacje zapraszał finalista Daj się poznać 2016. W możliwe najprostszy sposób przedstawił GraphQL w C# - czym jest i jak działa.

Bardzo ciekawy temat, zupełnie nie miałem z tym styczności, ale widać że jest potencjał w mechanizmie do formowania zapytań do naszego API. W wersji pod C# trochę jeszcze brakuje finalnych szlifów i wiele leży nadal na barkach developera (np. obsługa finalnych zapytań do SQL) to jest to ciekawa wiedza, którą można powoli wykorzystywać w praktyce w mniejszych projektach. 



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211030_0.jpg





### Enterprise ASP.NET -  Marcin Drobik


Wiele mówi się o nowościach pokroju .NET Core i innych cudach w świecie technologii z Redmond. Jednakże większość z nas nadal pracuje na projektach, które nie mogą tak szybko upgradeować się do najnowszych wersji. W tych sytuacjach zmartwieniem jest często architektura  w rozproszonym zespole.

Prezentacja przedstawiała trudności w wielo-wielowarstwowych aplikach i dużych zespołach, które w nich siedzą. Było trochę do śmiechu i refleksji (kto nie pracował na aplikacji, w której warstw było za dużo o co najmniej jedną?). Przedstawiono [Shotgun surgery](https://en.wikipedia.org/wiki/Shotgun_surgery) czy [silos techniczny](https://en.wikipedia.org/wiki/Information_silo) wraz z propozycjami na rozwiązanie tych problemów. Prezentacja zakończyła się ciekawymi wnioskami, z dzieleniem solucji per ficzer na czele i z chwilą zadumy w każdym z nas :)



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211031_0.jpg






### It&#39;s all about the state, czyli co skrywa async/await w C#? - Dariusz Pawlukiewicz


Techniczna prelekcja o elemencie języka, który wszedł wraz z C# 5. Można było dowiedzieć się  jak od strony CLI działają async/await i jak w to wszystko została wplątana maszyna stanowa.

Ciekawa prezentacja, która usatysfakcjonowała wiele osób lubiących niskopoziomowe niuanse platformy .NET.



![desk](https://raw.githubusercontent.com/djfoer/djfoxer.github.io/master/_img/2017-4-5-_13_/g_-_608x405_-_-_80333x20170404211033_0.jpg





## Podsumowanie

 
Konferencja wypchana była prezentacjami aż po brzegi. Każdy mógł znaleźć coś dla siebie od frontendowca, poprzez backend aż na architekcie aplikacji kończąc. Brakowało mi tylko odrębnej ścieżki SQL, chociaż może dobrze, że takowej nie było, gdyż byłoby zapewne jeszcze ciężej wybrać na co iść.

Mnogość prezentacja szła również z ich jakością (przynajmniej w ścieżkach .NET), aczkolwiek wydaje mi się, że można byłoby z kwotą rejestracyjną (300-400 zł) trochę zejść kosztem ilości prezentacji. Ogólnie jednak 4Developers oceniam pozytywnie i mam nadzieję, że za rok również uda mi się dostać na tą imprezę. Czekamy zatem na zapisy wideo wszystkich prezentacji.
