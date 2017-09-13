---
layout:     post
title:      Korelacja: sprzedaż czasopism - jakość &quot;pełniaków&quot; ?
date:       2011-07-15 23:12:00
summary:    W tym wpisie chciałbym, z czystej ciekawości sprawdzić, czy istnieje jakakolwiek korelacja pomiędzy sprzedażą czasopism, a atrakcyjnością (ocenami) pełniaków zawartych w nich.Do "badania" wziąłem dwa czasopisma: CD Action oraz PLAY!. Oba będąc w Związku Kontroli Dystrybucji Prasy udostępniają ilość ...
categories: <input id="chkTagsList_11" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_11" checked="checked" value="2048"><label for="chkTagsList_11">hobby</label> <input id="chkTagsList_12" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_12" checked="checked" value="4096"><label for="chkTagsList_12">inne</label>
---



W tym wpisie chciałbym, z czystej ciekawości sprawdzić, czy istnieje jakakolwiek korelacja pomiędzy sprzedażą czasopism, a atrakcyjnością (ocenami) pełniaków zawartych w nich.

Do "badania" wziąłem dwa czasopisma: CD Action oraz PLAY!. Oba będąc w Związku Kontroli Dystrybucji Prasy udostępniają ilość sprzedanych egzemplarzy. Dodatkowo, dzięki temu, iż są to magazyny o grach, łatwiej będzie sprawdzić oceny gier, niż gdyby były to czasopisma o oprogramowaniu.

 *Coś ze statystyki* 

Aby nie przedłużać i nie przynudzać wstępu o statystyce, krótko przedstawię pewne podstawowe pojęcia, pomocne w analizie tekstu (aczkolwiek nieobowiązkowe!).

Korelacja - siła zależność między zmiennymi
Współczynnik korelacji Pearsona  *p*  - znormalizowana miara (-1,1) określająca siłę korelacji; -1,1 - ścisła korelacja, 0 - brak korelacji.
Do  obliczenia współczynnika korelacji  *p* , potrzebna jest znajomość dwuwymiarowego rozkładu badanych cech dla danej populacji, a takich danych najczęściej nie posiadamy. Skutkiem tego jest, to iż korzystamy z estymatora  *r*  do oszacowania  *p*  , będącego współczynnikiem korelacji z próby.
Z racji tego, iż próba nie jest duża, skorzystamy z rozkładu t Studenta  ("uproszczony", bardzo popularny rozkład różnych statystyk, wyniki sprawdzamy w gotowej tabeli). 
Korzystając z t Studenta, ustalamy określony poziom istotności  *a*  (max. prawdopodobieństwo popełnienia błędu 1. rodzaju - odrzucenie hipotezy prawdziwej - (głównej)).
Hipotezy - szukając korelacji, w teorii sprawdzamy dwie hipotezy tzw. zerową i alternatywną. Zerowa w danym przypadku mówi o braku korelacji, zaś alternatywna o istnieniu powiązania. Odrzucenie hipotezy zerowej, skutkuje przyjęciem hipotezy alternatywnej.

Odrzucenie lub przyjęcie hipotezy, uzależniamy od wyliczonego  *t*  Studenta porównując go, z wartością  *ta*  - z tablicy t Studenta:
  *| t | >= ta*   - odrzucamy hipotezę H0
  *| t | < ta*   - brak podstaw do odrzucenia hipotezy H0

Tak to wygląda "na sucho". Po więcej zapraszam do genialnej książki "Statystyka matematyczna modele i zadania" - Jerzy Greń oraz na wikipedię ;) . 


 *Sprzedaż* 

Na początek, wyniki sprzedaży. Nikogo nie powinny zdziwić statystyki. CD Action od lat jest liderem prasy o grach, PLAY! ociera się już o granice wypłacalności. CD Action jest bardziej miarodajny niż PLAY!, które zostało wzięte do obliczeń jedynie jako ciekawostka i jako możliwość porównania danych ze statystykami CD Action. Dodatkowo PLAY! funduje czytelnikom prócz gier, które pochodzą "znikąd", to jeszcze często mają "czyszczenie magazynów" (pełne wersje gier z poprzednich miesięcy). Wiadomo, iż nie sprzyja to zwiększeniu sprzedaży.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-7-15-_182_/g_-_608x405_-_-_25771x20110714180415_1.png)


 *Wykres nr 1* 

Już teraz (w ramach rozgrzewki), można sprawdzić czy sprzedaż CD Action jest związana ze sprzedaży PLAY!?

Do dzieła:

H0 - hipoteza zerowa, brak korelacji między cechami (sprzedaż CD Action, a sprzedaż  PLAY!), dalej oznaczać będziemy jako  *p = 0* 
H1- hipoteza alternatywna, istnienie korelacji między cechami (sprzedaż CD Action, a sprzedaż PLAY!), dalej oznaczać będziemy jako  *p != 0* 

Poziom istotności ustalamy na  *a = 0,05* .

Korzystając z Excela (funkcja PEARSON, [wzór](http://office.microsoft.com/pl-pl/excel-help/pearson-HP005209210.aspx) ), obliczamy estymator  *r* 
 *r = 0,28 * 
Z racji małej próby (n = 16 miesięcy), obliczamy wartość statystyki t Studenta:
 *t = (r/sqrt(1-r^2)*)sqrt(n-2) = 1,07* 
wartość  *ta*  odczytana z tablic t Studenta ( *a = 0,05; a = 14 * ) to:  *2,14479* 
 *|t| = 1,07 < 2,14479 = ta*  - brak podstaw do odrzucenia hipotezy H0.

Podsumowując, nie wykryto zależności pomiędzy sprzedażą CD Action, a PLAY!  (co widać na wykresie;  wiadomo ćwiczenie na początek :P )

 *Pełniaki* 

Z owych 16 miesięcy wylistowałem pełne wersje gier, jakie były umieszczone w CD Action i PLAY!.
Problemem, mimo wszystko, okazała się ocena gier. Odpada szukanie pojedynczych recenzji i wyliczanie średniej. Również, oparcie się na jednej z większych polskich encyklopedii gier, nie było dobrym pomysłem (wiele słabych gier, ma zawyżone średnie). Wybór padł na [http://www.metacritic.com/](http://www.metacritic.com/). Strona zbiera recenzje i wylicza średnią (wykorzystywana jest np. na Steamie). Niestety nie wszystkie gry mają oceny, a niektóre gry nie figurują nawet w bazie. Mimo wszystko uznałem, iż lepszego wyjścia na chwilę obecną szybko nie znajdę.

Oto lista gier z ocenami w nawiasach:



## CD Action




sty-10 Watchmen: The End Is Nigh Part 1 (61), RollerCoaster 3 GOLD (81)
lut-10 Ninja Blade (61), So Blonde, Imperium Romanum (63)
mar-10 World of Goo (90), The Moment of Silence (70), Watchmen: The End Is Nigh Part 2 (44)
kwi-10 Blacksite: Area 51 (60), Drakensang: The Dark Eye (75), The Legend of Beowulf, DSJ 2
maj-10 Just Cause (75), Gwiezdne Wilki 2, Runes of Magic (71), Championship Manager 2008 (68)
cze-10 Act of War: Direct Action (82), Barrow Hill (65), Brothers in Arms: Road To Hill 30 (87)
lip-10 Ghost Recon Advanced Warfighter (80), Battlestations: Midway (76), Ford Racing 3 
sie-10 Conflict: Denied Ops (58), Piraci Nowego Świata 2 (48), SBK 09 (71)
wrz-10 Tom Clancy’s Rainbow Six Vegas (85), Hitman Trylogia (73, 87, 74), Ford Racing Off Road (39)
paź-10 King’s Bounty: Legend (79), Cryostasis (69), Darkness Within: In Pursuit of Loath Nolder (52)
lis-10 Dark Messiah of Might and Magic (72), Necro Vision (63), Sublustrum (63)
gru-10 Tomb Raider: Legend (82), Lost Via Domus (52)
sty-11 Kane & Lynch: Dead Men (67), Resident Evil 4 (76)
lut-11 Tomb Raider: Anniversary (83), Devil May Cry 3 (66)
mar-11 Braid (90), SBK X (73), Thief Trylogia (92, 85, 87)
kwi-11 Call of Juarez: Bound in Blood (78), Bionic Commando (69), Shaun White Snowboarding (60), Allods Online (69)




## PLAY!




sty-10 Tension (77), Tecno: The Base, Valkyrie: Ascension to the Throne 
lut-10  *Czyszczenie magazynów! :/* 
mar-10 9th Company, Shadowgrounds (74), Kurka w ogniu
kwi-10  *Czyszczenie magazynów! :/* 
maj-10 Arcanum (81), Clutch (51), Outpost Kaloki, Runes of Magic (71)
cze-10  *Czyszczenie magazynów! :/* 
lip-10 Gothic 3 (63), Velvet Assassin, The Path (61), Runes Of Magic (71)
sie-10 Planescape Torment (91), Alliance: Globalny konflikt (43), Shadowgrounds Survivors (79)
wrz-10 Infernal (61), Ceville (73), German Truck Simulator
paź-10 Venetica (61), Chrome (73), Spells of Gold
lis-10 Zeno Clash (77), Adrenalin
gru-10  *Czyszczenie magazynów! :/* 
sty-11 X-Blades (54), Chrome (62), Super Stunt Spectacular
lut-11 Vampire Hunters, Age of Pirates (56), Penumbra: Czarna Plaga (78)
mar-11 Trine (80), Alpha Prime (59), Vivisector
kwi-11 Warfare, Steam Slug, Grupa Błyskawicznego Reagowania


Dane odnośnie ocen pełnych wersji zamieszczonych w PLAY! nie nadają się zbytnio do analizy. Częste "czyszczenie magazynów" oraz mało znane gry, uniemożliwiają wiarygodną analizę korelacji. Mimo wszystko, zebrane dane umieściłem na wykresach z danymi CD Action. 

 *Pełniaki - średnia ocen pełnych wersji * 


Przystępujemy do ciekawszych obliczeń :)
Na podstawie zebranych danych sprawdzimy, czy istnieje zależność pomiędzy sprzedażą CD Action, a pełnymi grami dorzucanymi do czasopisma (średnie oceny z każdego miesiąca)?

Na wykresie nr 2 przedstawiono średnie oceny z pełnych wersji gier. 
Dla ciekawości dodam, że średnia z całego okresu 16 miesięcy wynosi 70.

H0 - hipoteza zerowa, brak korelacji między cechami (sprzedaż CD Action, a średnia ocena pełnych wersji gier),   *p = 0* 
H1- hipoteza alternatywna, istnienie korelacji między cechami (sprzedaż CD Action, a średnia ocena  pełnych wersji gier),  *p != 0* 

Poziom istotności ustalamy na  *a = 0,05* .
obliczamy estymator  *r* 
 *r = -0,40 * 
obliczamy wartość statystyki t Studenta:
 *t = (r/sqrt(1-r^2)*)sqrt(n-2) = -1,65* 
wartość  *ta*  odczytana z tablic t Studenta ( *a = 0,05; a = 14 * ) to:  *2,14479* 
 *|t| = 1,65 < 2,14479 = ta*  - brak podstaw do odrzucenia hipotezy H0.




## Podsumowując, nie wykryto zależności pomiędzy sprzedażą CD Action, a średnią ocena  pełnych wersji gier 






![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-7-15-_182_/g_-_608x405_-_-_25771x20110714180415_2.png)


 *Wykres nr 2 / Wykres nr 3* 

 *Pełniaki - mediana ocen pełnych wersji * 


Bardzo podobny punkt, jak poprzedni, jedynie zamiast obliczać średnią ocen gier z miesiąca, obliczamy medianę. A zatem: czy istnieje zależność pomiędzy sprzedażą CD Action, a pełnymi grami dorzucanymi do czasopisma (mediana oceny z każdego miesiąca)?

Dane przedstawione na wykresie nr 3, mediana z całego roku wynosi: 71.

H0 - hipoteza zerowa, brak korelacji między cechami (sprzedaż CD Action, a mediana ocen pełnych wersji gier),   *p = 0* 
H1- hipoteza alternatywna, istnienie korelacji między cechami (sprzedaż CD Action, a mediana ocen  pełnych wersji gier),  *p != 0* 

Poziom istotności ustalamy na  *a = 0,05* .
obliczamy estymator  *r* 
 *r = -0,38 * 
obliczamy wartość statystyki t Studenta:
 *t = (r/sqrt(1-r^2)*)sqrt(n-2) = -1,52* 
wartość  *ta*  odczytana z tablic t Studenta ( *a = 0,05; a = 14 * ) to:  *2,14479* 
 *|t| = 1,52 < 2,14479 = ta*  - brak podstaw do odrzucenia hipotezy H0.




## Podsumowując, nie wykryto zależności pomiędzy sprzedażą CD Action, a medianą ocen  pełnych wersji gier (można było się spodziewać, analizując średnią ocen i wykresy dla obu statystyk (wykres nr 2 i 3)) 





 *Pełniaki - pełna wersja z najwyższą oceną za dany miesiąc * 

Na koniec sprawdzamy: czy istnieje zależność pomiędzy sprzedażą CD Action, a pełnymi grami dorzucanymi do czasopisma (maksymalna (najwyższa) ocena z każdego miesiąca) 

H0 - hipoteza zerowa, brak korelacji między cechami (sprzedaż CD Action, a najwyższa ocena pełnej wersji),   *p = 0* 
H1- hipoteza alternatywna, istnienie korelacji między cechami (sprzedaż CD Action, a najwyższa ocena pełnej wersji)),  *p != 0* 

Poziom istotności ustalamy na  *a = 0,05* .
obliczamy estymator  *r* 
 *r = -0,60* 
obliczamy wartość statystyki t Studenta:
 *t = (r/sqrt(1-r^2)*)sqrt(n-2) = -2,80* 
wartość  *ta*  odczytana z tablic t Studenta ( *a = 0,05; a = 14 * ) to:  *2,14479* 
 *|t| = 2,80 > 2,14479 = ta*  - odrzucamy hipotezę H0, o braku korelacji.

Bingo! Trafiony zatopiony. 
Podsumowując ten krok: możemy założyć, iż istnieje korelacja (powiązanie), pomiędzy sprzedażą magazynów z grami (na przykładzie CD Action), a najwyżej ocenianą grą z danego miesiąca.

Wykres nr 5 - przedstawia wykres dwóch cech: sprzedaż X ocena. Poprowadzono linie trendu. Widać, iż dla danych z maksymalną oceną, występuje korelacja.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-7-15-_182_/g_-_608x405_-_-_25771x20110715222214_3.png)


 *Wykres nr 4 / Wykres nr 5* 

 * Najważniejsze - interpretacja * 


Obliczenia pokazały, iż na sprzedaż magazynów z pełnymi wersjami (w naszym przypadku CD Action) wpływ ma maksymalna ocena gry (najwyżej oceniana) z danego miesiąca. 
UWAGA! Estymator korelacji otrzymaliśmy ze znakiem ujemnym! Co z tego wynika? Oznacza to, iż sprzedaż CD Action do najwyżej ocenionej gry, jest odwrotnie proporcjonalna! Czyli im w miesiącu pełna wersja gry, która ma najwyższą ocenę, jest lepsza, tym sprzedaż jest mniejsza!
Dziwne? Dane nie kłamią :) Nie jest to również nielogiczne.
Jeśli czasopismo zamieszcza pełną wersję gry, która posiada bardzo wysokie oceny, nie może zamieścić bardzo nowej gry, z przyczyn czysto ekonomicznych. A zatem, idąc dalej. Zamieszczenie takiej gry może okazać się strzałem w kolano. Gra która powinna napędzać sprzedaż nie robi tego. Dlaczego? Możliwe, iż ze względu na to, że jako gra mająca świetne oceny, została już kupiona wcześniej, właśnie z tego powodu, przez większą część graczy. Ci co jej nie kupili, sugerując się dobrymi ocenami, pożyczyli ją już wcześniej lub, niestety, zaopatrzyli się w piraty (co niestety jest nadal problemem).
(Patrz: sprzedaż (Wykres 1) / maksymalna ocena (Wykres nr 4) za miesiąc: marzec 2010, czerwiec 2010, grudzień 2010, marzec 2011 - dobre oceny maksymalne - słaba sprzedaż).

Co w takim razie dzieje się z drugiej strony?
Sprzedaż gier "średnich" (ale nie "kaszanek" jak w PLAY!) powoduje wzrost sprzedaży (patrz wykresy 1 i 4 za miesiąc: luty 2010, kwiecień 2010, styczeń 2011). Osoby kupujące gry nie chcą kupować podczas premiery średniaków, gdyż wolą wydać pieniądze na lepsze gry. Co za tym idzie. Widząc grę w czasopiśmie za mniejsze pieniądze z chęcią kupią coś, co może nie jest hitem (a może właśnie im się spodoba?),  ale nie posiadają w swojej kolekcji. 

Proszę zauważyć dwukrotny wzrost sprzedaży PLAY! w lipcu 2010, mimo średnich wyników. Powód? Ciekawe gry (The Path) lub sequele prawdziwych hitów (Gothic 3), ale mające średnie recenzje. 



Obliczenia dały naprawdę ciekawe i, jak dla mnie, zaskakujące wyniki. Temat nie jest zamknięty. Już teraz, mam kilka pomysłów jak go rozwinąć. Dodanie większej ilości danych, nowe, bardziej miarodajne cechy do porównania. 

Dane z magazynu PLAY! posłużyły jedynie do celów porównawczych na wykresach. Oceny nie różnią się może zbytnio od siebie (Wykres nr 2), ale w PLAY! część gier jest na tyle słaba, iż nie ma ocen. Zaś o "czyszczeniu magazynów" nawet nie wspomnę ;)

Wpis okazał się bardzo interesujący i pożyteczny(? :P). Zaznaczam, iż mogą gdzieś pojawić się błędy w obliczeniach/statystykach. Jeśli coś, piszcie śmiało. Dzięki temu wpisowi przypomniałem sobie czasy statystyki ze studiów i (jakkolwiek by to zabrzmiało) w sumie nieźle się bawiłem :D.


 *Pozdrawiam* 
