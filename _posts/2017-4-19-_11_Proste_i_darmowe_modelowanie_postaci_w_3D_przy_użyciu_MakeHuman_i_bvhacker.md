---
layout:     post
title:      Proste i darmowe modelowanie postaci w 3D przy użyciu MakeHuman i bvhacker
date:       2017-04-19 20:58:00
summary:    Modelowanie w 3D wydaje się nietrywialnym zagadnieniem. Na przeszkodzie staje nie tylko brak umiejętności i doświadczenia, ale także elementy bardziej materialne. Często ograniczeniem bywa sprzęt, który nie uciągnie aplikacji do grafiki 3D, ale również oprogramowanie, które potrafi słono kosztować.W tym wpisie pragnę przedstawić szybki sposób na modelowanie postaci 3D. Nie będzie wymagana znajomoś...
categories: windows oprogramowanie porady
---



Modelowanie w 3D wydaje się nietrywialnym zagadnieniem. Na przeszkodzie staje nie tylko brak umiejętności i doświadczenia, ale także elementy bardziej materialne. Często ograniczeniem bywa sprzęt, który nie uciągnie aplikacji do grafiki 3D, ale również oprogramowanie, które potrafi słono kosztować.

W tym wpisie pragnę przedstawić szybki sposób na modelowanie postaci 3D. Nie będzie wymagana znajomość zagadnień grafik 3D, a oprogramowanie użyte do tego wpisu jest całkowicie darmowe, również do celów komercyjnych. Dodatkowo przedstawione aplikacje nie wymagają kosmicznego sprzętu, aby móc wygodnie pracować, jednocześnie osiągając zadowalające wyniki.



## Modelowanie postaci w 3D - prosty przepis dla każdego

Zacznę od tego, że nigdy nie wiemy, kiedy może przydać się nam wymodelowanie postaci w 3D. Do tej pory temat grafiki 3D omijałem szerokim łukiem, gdyż jako programista aplikacji nie widziałem zastosowania tej dziedziny w swojej branży. Okazało się, że szybko zmienię zdanie.

Zapewne nie tylko osoby tworzące animacje czy wizualizacje mogą potrzebować szybkiej i bezproblemowej edycji modelu postaci w 3D. Może się okazać, że ktoś z was będzie robił aplikację do nauki golfa czy ćwiczeń i będzie zmuszony do grzebania się w grafice trójwymiarowej.

Tworząc na konkurs wtyczkę do Visual Studio ([Healthy with Visual Studio](https://www.dobreprogramy.pl/djfoxer/Healthy-with-Visual-Studio-wtyczka-ktora-zadba-o-zdrowie-i-czas-dewelopera,79587.html) — wtyczka, która zadba o zdrowie i czas dewelopera) okazało się, że będę musiał pozyskać kilka modeli 3D. Jako iż dodatek miał prezentować wybrane ćwiczenia do rozciągania się przy komputerze, niezbędne było stworzenie postaci w grafice trójwymiarowej w odpowiednich pozycjach.

Potrzebowałem aplikacji, która będzie darmowa do dowolnego użytku, nie będzie wymagała znajomości grafiki 3D i będzie miała wbudowane modele. Dodatkowo musiałem mieć możliwość tworzenia różnych pozycji. Zatem program powinien oferować także poruszanie całym szkieletem, w celu ustawienia odpowiedniej pozy postaci.

Znalezienie takiej aplikacji nie okazało się wcale proste. [Blender](https://www.blender.org/) był pierwszym pomysłem, ale nie miałem ochoty zaczynać zabawy z modelowanie od zera i zabawą z wtyczkami i innymi rzeczami. [DAZ Studio](https://www.daz3d.com/home) był ciekawy, ale darmowa licencja raczej zniechęca do użycia czegokolwiek poza własną satysfakcje. [DesignDoll](http://terawell.net/terawell/) oferował za mało w wersji bezpłatnej, a [Poser](http://my.smithmicro.com/poser-11.html) wydawał się ciekawy, ale kosztowny. Na szczęście znalazłem aplikacje, która idealnie trafiła w moje potrzeby...



## MakeHuman - trywialne modelowanie postaci 3D


Przeglądając sieć natrafiłem na rewelacyjny projekt - [MakeHuman](http://www.makehuman.org). Jest to całkowicie darmowa i otwarta inicjatywa, której celem jest jak najprostsze tworzenie zaawansowanych modeli postaci w 3D.  


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419200203_0.jpg)


MakeHuman oferuje olbrzymie możliwości w modelowaniu postaci. Na początku otrzymujemy domyślny model. Za pomocą suwaków i przełączników określamy płeć, wiek, wysokość, proporcje ciała czy pochodzenie etniczne. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419202031_0.png)


W kolejnych krokach możemy uszczegółowić cechy związane z płcią, najdrobniejszymi elementami twarzy, korpusu, rąk czy nóg. Jest tego bardzo dużo, ale nie sposób zgubić się gąszczu opcji. Wszystkie elementy są świetnie opisane i mają graficzny opis.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419202031_1.png)


Możemy także ubrać naszą postać i wybrać pozycję. Dodatkowo jest opcja umiejscowienia "szkieletu" w naszym modelu. W ten sposób można edytować postawę w innych aplikacjach. Na koniec nadamy odpowiednie tło, umiejscowimy światła i wyrenderujemy gotowy model.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419202032_1.png)


Opcji jest multum i jeśli chodzi o stworzenie modelu postaci to możliwości są niemalże nieograniczone. Dodatkowo końcowy efekt można przenieść chociażby do Blendera i tam kontynuować pracę z innymi obiektami. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419202032_0.png)


Niestety w obecnej wersji MakeHuman nie ma jednej, bardzo potrzebnej opcji. Można nanosić różne pozy dla naszego modelu (zawarte w aplikacji), ale nie jesteśmy w stanie edytować szkieletu. Forum sugeruje, aby gotowy model przenieść do Blendera i tam ustawić odpowiednią pozycję, ale nie chciałem odpalać kombajnu do tak nieskomplikowanej operacji. Zatem do edycji szkieletu użyjemy...


## Bvhacker - edycja i animacja szkieletu


[Bvhacker](http://www.bvhacker.com/) jest całkowicie darmową aplikacją do tworzenia animacji i edycji szkieletu modelu. Program opiera się na tekstowych plikach BVH, które opisują szkielet postaci. Program nie jest już rozwijany, ale obecna wersja 1.8 działa wyśmienicie do prostych zastosowań.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419203431_0.png)


Po wczytaniu pliku na środku okna mamy model edytowanego szkieletu. Po lewej wybieramy z drzewka element ze szkieletu do zmiany, a wartości wirtualnej kości zmieniamy po prawej stronie. W zasadzie to tyle i aż tyle. Bywają problemy z ustawieniem modelu w 3D, ale reszta działa wyśmienicie. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419202510_0.png)


W celu edycji szkieletu z MakeHuman wystarczy, że wyedytujemy pliki bvh z tej aplikacji wedle naszych potrzeb (folder  *\data\poses* ). Po zapisaniu zmian MakeHuman sam naniesie nową pozę na model (zakładka  *Pose/Anime* ).


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419204244_0.png)



## Healthy with Visual Studio

Tworzona wtyczka do Visual Studio otrzyma zatem  niedługo możliwość wyświetlania ćwiczeń. Warto śledzić kolejne etapy tworzenia dodatku. Zapraszam. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419204244_1.png)



> Źródła dostępne są na GitHubie (branch master i POC):
> [https://github.com/djfoxer/healthyWithVS/](https://github.com/djfoxer/healthyWithVS/)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-4-19-_11_/g_-_608x405_-_-_80604x20170419204356_1.png)

