---
layout:     post
title:      dobreprogramy mini w jQuery Mobile - wersja mobilna (update 7; 16.01.13)
date:       2012-02-06 22:36:00
summary:    W tamtym tygodniu qbap opisał we wpisie dobreprogramy w wersji mini swoją wizję portalu w wersji mobilnej, całkiem przypadkiem zbiegło się to z moim wpisem jQuery Mobile - programowanie mobilne. Postanowiłem połączyć dość luźno te oba wpisy i stworzyć coś co mogłoby się przydać dla każdego z nas. Tak oto powstała wersja www dobrychprogramów na urządzenia przenośnie stworzona w jQuery Mobile. Jest ...
categories: oprogramowanie internet urządzenia mobilne
---



W tamtym tygodniu qbap opisał we wpisie [dobreprogramy w wersji mini](http://www.dobreprogramy.pl/qbap/dobreprogramy-w-wersji-mini,30118.html) swoją wizję portalu w wersji mobilnej, całkiem przypadkiem zbiegło się to z moim wpisem [jQuery Mobile - programowanie mobilne](http://www.dobreprogramy.pl/djfoxer/jQuery-Mobile-programowanie-mobilne,30130.html). Postanowiłem połączyć dość luźno te oba wpisy i stworzyć coś co mogłoby się przydać dla każdego z nas. Tak oto powstała wersja www dobrychprogramów na urządzenia przenośnie stworzona w jQuery Mobile. Jest to dużo bogatsza wersja niż [m.dobreprogramy.pl](http://m.dobreprogramy.pl/).

Wersja działająca dostępna jest pod adresem: [www.djfoxer.pl/mini/](http://www.djfoxer.pl/mini/)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120206222317_0.jpg)
[join]
![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120206222325_0.jpg)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120206222335_0.jpg)
[join]
![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120206222351_0.jpg)


Zapraszam do wyrażenia krytycznej opinii, wskazówek itp.


## Cechy dobrychprogramów mini





  * możliwość przejrzenia 10 ostatnich wpisów (skróconych) z działu: Aktualności, Lab, Blog, Programy, Programy - testowe



  * malutki rozmiar strony: 2 KB (strona html) + 10 KB (lista 10 wpisów), reszta jest w cache (pobierane tylko za pierwszym razem)



  * pobranie wskazanych, PEŁNYCH TREŚCI WPISÓW z działu Aktualności (jeden pełny wpis to ok. 3 KB!)



  * bezpośredni link do każdego wpisu



  * działa na większości mobilnych przeglądarek, sprawdzane na : Internet Explorer 9 (WP7), Opera Mobile 11.5 (Emulator for Windows), Fennec 4.0.1 (Windows)



  * uniwersalny interface z jQuery Mobile




## Opis


Strona jest prosta i bardzo mała. Na górze umieściłem combobox, z którego można wybrać, który dział chcemy załadować: Aktualności, Lab, Blog, Programy, Programy - testowe (domyślnie ładowane są Aktualności). W danym momencie, jeśli raz wczytamy dział jest on zapamiętywany na czas "sesji", podobnie pełne artykuły z Aktualności (jest to jedna strona więc dane trzymane są w JavaScripcie, narazie nie w ciasteczkach). 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120206222907_0.jpg)
[join]
![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120206222915_0.jpg)




Dzięki stworzeniu strony w jQuery Mobile, jest ona mała, przystosowana do działania na urządzeniach mobilnych i całkiem ładna ;) Jeśli przeglądarka wspiera cache (czyli większość mobilnych), wejście na stronę i pobranie 10 Aktualności w wersji skróconej to ok. 12 KB. Pobrany, pełny wpis na życzenie, to ok. 3KB. Nie jest to dużo i można zaoszczędzić na łączu.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_608x405_-_-_30176x20120206222237_0.png)



### Subskrypcje


W menu wyboru widoczna jest opcja "Subskrypcje". Nie jest ona jeszcze oprogramowana. W sumie liczę na jakiś odezw, czy jest sens ją robić, czy będzie jakieś zainteresowanie. W założeniach mają być tam wybrane kanały RSS blogerów na dobrychprogramach. W sumie to wyglądać będzie jak mały czytnik RSS. Z poziomy dobrychprogramów mini, byłaby możliwość dodawania/usuwania/edycji kanałów RSS blogerów. Pytanie: "jest sens to robić"?


## Chętni?


Zapraszam do testów na [www.djfoxer.pl/mini/](http://www.djfoxer.pl/mini/) i wyrażenie swojej opinii tutaj (mam nadzieje, że komuś się to przyda).




## Update 1 (v. 0.1.0.1, 07.02.2012)


Zmiany jakie dodałem dzięki Waszemu zaangażowaniu :)



  * nie będzie już ucinać napisu "dobreprogramy" w nagłówku


  * "dobre" "programy" zyskał nowy image ;)


  * wyjustowanie tekstu




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_608x405_-_-_30176x20120207175821_0.jpg)

Sprawdziłem też wyświetlanie na Operze Mini (6.5 i 4.2)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120207175031_0.jpg)
[join]
![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120207175037_0.jpg)


"Otwieranie" nowego okna, po wybraniu z menu, jest spowodowane tym, iż wysokość okna przglądarki www jest za mała. jQuery Mobile, w takim przypadku, daje tło, aby opcje wyboru były bardziej widoczne. Można to zaobserwować, też na "dużych" przeglądarkach, zmniejszając okno.

Jeśli chodzi o Amazon Kindle ,to problem jest pewnie w interpretacji w znaczniku "a" z atrybutem "target=' _blank' ". Coś pokombinuje, aby znaleźć złoty środek, bo lepiej jak okno z odnośnikiem do artykułu na dobreprogramy.pl otwiera się w nowym oknie.

Postaram się dodać niedługo wyświetlanie komentarzy (tylko do aktualności?).


## Update 2 (v. 0.2, 09.02.2012)


Dzięki za uwagi jakie zgłosiliście.

Wrzuciłem na serwer nową wersje, całkiem sporo zmian (m.in komentarze):



  * pobieranie pełnych treści dla Aktualności, Labu i Blogów


  * pobieranie komentarzy dla Aktualności, Labu i Blogów


  * ukrywanie sekcji z pobranymi danymi


  * zmniejszenie danych pobieranych podczas ściągania pełnych treści artykułów


  * przejdź do strony, przechodzi bezpośrednio do artykułu, nie otwiera nowego okna


  * usunięcie pogrubienia dla treści wpisów
 

  * nowy skin
 

  * "usunięcie" Subskrypcji


  * jQuery hostowane na google




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_608x405_-_-_30176x20120209231853_0.jpg)



## Update 3 (v. 0.2.1, 10.02.2012)




  * dodano graficzną reprezentację ilości komentarzy


  * usunięto "Programy w wersji testowej"




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_608x405_-_-_30176x20120210180150_0.jpg)



## Update 4 (v. 0.2.4, 20.02.2012)





  * poprawiono wyświetlanie komentarzy


  * dodano zmaczniki nowej linii dla wpisów i komentarzy


  * dodano formatowanie składni (code)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120221075911_0.jpg)
[join]
![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-6-_149_/g_-_288x192_-_-_30176x20120221075920_0.jpg)





## Update 5 (v. 0.3.0, 29.06.2012)





  * wyrzucenie api googla do wstępnego ściągania rssów


  * pobieranie z labu "specjalnych" recenzji


  * zmniejszenie ilości pobieranych danych
 



## Update 6 (v. 0.4.0, 28.01.2013)





  * poprawka z wyświetlaniem przyrostków w nicku (redakcja, moderator bloga itp.) - zgłosił Quest


  * aktualizacja jQuery do 1.8.2


  * aktualizacja jQuery Mobile do 1.2.0




## Update 6 (v. 0.4.2, 16.02.2013)





  * pobieranie treści dla blogów z kategorii "pozostałe"


  * menu select do wybierania treści, zostało przekształcone w natywny select (kompatybilność ze starszymi przeglądarkami)

