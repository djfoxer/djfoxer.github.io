---
layout:     post
title:      Rockbox - rewelacyjny firmware do przenośnych odtwarzaczy muzyki
date:       2012-05-17 23:09:00
summary:    Wgrywanie nieoficjalnych, alternatywnych firmwareów stało się rzeczą normalną i nikogo nie dziwi, że oprogramowanie wbudowane w urządzenie, zastępowane jest softem stworzonym poza firmą, która dostarczyła sprzęt. Routery, telefony komórkowe, odtwarzacze DVD, konsole, aparaty cyfrowe... wszędzie tam ...
categories: sprzęt oprogramowanie urządzenia mobilne
---



Wgrywanie nieoficjalnych, alternatywnych firmwareów stało się rzeczą normalną i nikogo nie dziwi, że oprogramowanie wbudowane w urządzenie, zastępowane jest softem stworzonym poza firmą, która dostarczyła sprzęt. Routery, telefony komórkowe, odtwarzacze DVD, konsole, aparaty cyfrowe... wszędzie tam można wgrać niewspierany firmware, który często posiada dodatkowo możliwości, nieoferowane przez oryginalne oprogramowanie. W tym wpisie, postaram się przedstawić bardzo ciekawe oprogramowanie do przenośnych odtwarzaczy muzyki ( potocznie zwanymi mp3kami, czy mp4kami ) - [Rockbox](http://www.rockbox.org/). 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_608x405_-_-_31656x20120515220424_0.jpg)





## Rockbox

  



Wydaje się, że firmware do przenośnych odtwarzaczy muzyki, nie może oferować wielu nowych, ciekawych opcji. Tak też myślałem, przed wrzuceniem Rockboxa na moją MP3ke. To co udostępnia Rockboxa robi ogromne wrażenie. Poczynając od instalacji, poprzez konfigurację, aż do codziennego użytkowania - wszytki jest zrobione wzorowo i bardzo profesjonalnie. Mając odtwarzacz z Rockboxem, można dojść do wniosku, iż zamienił się on w mały komputerek, z ogromem opcji, niedostępnych nigdzie indziej.




## Urządzenia kompatybilne z Rockbox



Rockbox jest ciągle rozwijany od 2001 roku. Obecnie, wersja stabilna  może być zainstalowana na 32 najbardziej popularnych przenośnych odtwarzaczach muzyki. Kolejne 31 urządzeń jest w fazie developingu i w najbliższym czasie, można będzie się spodziewać wydania wersji stabilnych. Co ciekawe, trwają również prace nad przeniesieniem Rockboxa, na jeszcze większą ilość sprzętu. Na stronie, Twórcy udostępniają listę urządzeń (obecnie 63!), które są na etapie &quot;rozkładania na czynniki pierwsze&quot; i wstępnej analizy. Wszystkie urządzenia, na etapach, o których wspomniałem, dostępne są na stronie [Rockbox Status on Various Targets](http://www.rockbox.org/wiki/TargetStatus).

Cieszy to, iż każde urządzenie ma oddzielną podstronę w formie &quot;wiki&quot;, gdzie znajdziemy opis instalacji, wszelkie informacje o porcie, zdjęcia z rozkładania odtwarzaczy, porady, listy TODO,  specyfikacje sprzętowe, porównania sprzętowe, dedykowane aplikacje... jest tego bardzo dużo i dla zainteresowanych, będzie to stanowić interesujące źródło wiedzy. 



## W praktyce



W kilku akapitach omówię działanie i moduły Rockboxa w wersji 3.11.2  na SanDisk Sansa Clip+. Na potrzeby wpisu przetestowałem działanie zarówno na ww. urządzeniu, ale także na emulatorze Sansy Clip+ i iPoda Color.



### Instalacja



W większości alternatywnego oprogramowania, wgranie firmwareu wymaga bardziej zaawansowanej znajomości komputera/urządzenia. W przypadku Rockboxa, instalacja oprogramowania jest bardzo prosta i szybka. Sprowadza się ona do podłączenia urządzenia i odpalenia Rockbox Utility. Program sam potrafi wykryć urządzenie, a cała operacja sprowadza się do kliknięcia na &quot;Kompletna instalacja&quot;. W ten sposób zainstalujemy pełną wersję firmwareu. W niektórych przypadkach będzie konieczność podania oryginalnego pliku z firmwarem (nie mogą być one rozpowszechniane, ze względu na licencje), co wiąże się jedynie z kliknięciem na link zaproponowany przez instalator.

Rockbox instaluje się obok oryginalnego oprogramowania. W każdej chwili można przełączyć się pomiędzy wersjami firmwareu lub usunąć nowy soft.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_608x405_-_-_31656x20120515222925_0.png)






### Pierwsze chwile z Rockboxem



Wszystkie wersje, bez względna na urządzenie na jakim się zainstaluje, wyglądają dość podobnie. Czy to iPad Color z kolorowym, dużym wyświetlaczem, czy Sansa Clip+ z dwukolorowym małym ekranem, funkcjonalności są niemalże identyczne.

Ekran jest czytelny, a opcje poukładane dość logicznie. Momentami można jednak się pogubić, a sterowanie nie zawsze jest w każdym podmenu identyczne. Na początek może trochę odstraszyć, ale jeśli damy mu szanse, dostaniemy potężne oprogramowanie do naszego malucha.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120515223954_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120515223959_0.png)






![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120517175601_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120517175607_0.png)







### Ustawienie dźwięku





Możliwości konfiguracji dźwięku są bardzo duże, standardowo otrzymujemy

  * konfigurację: głośności/basów/tonów wysokich/balansu,


  * ustawienie kanałów (w tym karaoke!),
 

  * zmiana szerokości stereo,
 

  * crossfeed (mieszanie kanałów stereo), plus zmiana wzmocnienia głównego/skośnego, tłumienie tonów wysokich,  ustawienie górnej częstotliwości granicznej,


  * korektor 5 pasmowy, możliwość wczytania kilku zdefiniowanych profili (wg. mnie te domyślne są świetne), wzmacnianie pasm, zaawansowane ustawienia filtrów pasmowych, górnoprzepustowych...


  * dithering - delikatne poprawienie dźwięku, faktycznie dźwięk wydaje się być lekko wyraźniejszy


  * ustawienie szybkości


  * kompresor - normalizacja dynamiki utworu




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120515231454_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120515231458_0.png)





### Odtwarzanie dźwięku



Rockbox oferuje ogromną ilość wspieranych formatów plików: MPEG (MP3/MP2/MP1), Ogg Vorbis, MPEG-4 AAC, Musepack, AC3, WMA, Speex, Cook, ATRAC3, WavPack, FLAC, WavPack, Shorten, Apple Lossless, Monkey&#39;s Audio, TTA, Intel WAV, Apple AIFF. Odtwarza także formaty związane z grami, takie jak:  ADX, SID, NSF, SAP, SPC, AY, GBS, HES, KSS, MOD, SGC, VGM, VGZ,  Yamaha SMAF. Robi wrażenie.

Już nie będę oczywiście wspominał o losowym odtwarzaniu, kilku opcjach powtarzania utworów, wielu możliwościach przewijania, ale warto wspomnieć np. 

  * wsparcie dla Last.fm i plików CUE,


  * normalizacji głośności piosenek (ReplayGain),


  * płynnego odtwarzania (Gapless playback),


  * płynne przejście pomiędzy piosenkami (Crossfade),


  * detekcja odłączenia słuchawek  (i np. włączenie pauzy),
 

  * party mode.

Oczywiście  opcji jest jeszcze więcej...



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120515235802_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120515235805_0.png)





### Nagrywanie dźwięku



Oczywiście nie mogło obyć się bez nagrywania dźwięku. Rocbox i w tym nie zawiódł. Oferuje on możliwość zapisu do PCM Wave, AIFF, WavPack, MP3, wybór kanału, czy częstotliwości. Nagrane mogą być dźwięki z zewnątrz, za pomocą mikrofonu lub rejestrowane audycji z radia. Z ciekawszych rzeczy - istnieje opcja automatycznego dzielenia plików (po osiągnięciu określonego rozmiaru/długości), a także automatycznego wywoływania nagrywania! Można ustawić parametry dźwięku, przy jakich zapis rozpocznie się automatycznie. 




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516230403_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516230406_0.png)





### Wtyczki - Gry



Wraz z nowym oprogramowaniem na nasz odtwarzacz, otrzymujemy zestaw gier. Jest ich całkiem sporo i każdy znajdzie coś dla siebie. Sterownia nie jest tak intuicyjne jak na PSP, ale daje radę :) Mamy zatem szachy, jednorękiego bandytę, karty, pong, sapera, reversi, węża, a nawet... DOOMA (działa też na Sansie :D )!!



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516231949_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516231942_0.png)





### Wtyczki - aplikacje



Kolejny zbiór wtyczek to aplikacje. Znajdziemy tu m.in. edytor tekstu (!), aplikację do strojenia gitary, stoper, kalkulator, alarm, kalendarz.... Pamiętacie nadal, że to &quot;tylko&quot; odtwarzacz mp3? :)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516232629_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516232635_0.png)






### Wtyczki - demonstracje



Kilka dodatków, które pozwolą nam sprawdzić na co stać naszego &quot;malucha&quot; lub pomóc rozładować baterię. Mamy tu: animację ognia, fraktale, obiekty pseudo 3D i masę innych zapychaczy.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516233115_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516233119_0.png)





### Style



Do każdego odtwarzacza, z poziomu Rockbox Utility, istnieje opcja pobrania styli. Ogólnie tematów jest bardzo dużo, w zależności od odtwarzacza. Instalacja sprowadza się do wybrania skórki z przeglądarki i kliknięcia na przycisk. Style są plikami XML, więc nic nie stoi na przeszkodzie, aby samemu stworzyć taką skórkę.




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_608x405_-_-_31656x20120516233507_0.png)





### Pozostałe opcje



Oczywiście opcji jest jeszcze więcej, wymienię tylko te bardzie ciekawsze i unikatowe:

  * możliwość instalacji &quot;syntezatora mowy&quot;, dzięki czemu Rockbox, będzie czytał menu wraz z przemieszczaniem się po nim!,


  * wyświetlanie aktualnej godziny,


  * wiele ustawień ekranu,


  * wiele języków,


  * odtwarzacz multimediów - obrazów i filmów,


  * wpisywanie tekstu alfabetem morse&#39;a! (zamiast klawiatury ekranowej),


  * eksplorator plików,


  * robienie screenów.




##  Emulator



Zanim wgramy Rockboxa na odtwarzacz, warto go przetestować. Twórcy dali nam emulatory aż 56 urządzeń, na których możemy &quot;na sucho&quot;, sprawdzić jak nowe oprogramowanie będzie radziło sobie z naszym sprzętem ([Rockbox simulator builds](http://rasher.dk/rockbox/simulator/)). Idealne np. przed zakupem, aby sprawdzić które wspierane urządzenie, najbardziej pasuje nam razem z Rockboxem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516235143_0.png)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-5-17-_134_/g_-_288x192_-_-_31656x20120516235311_0.png)





## Na koniec



Rockbox to alternatywny firmware z najwyższej półki i do tego darmowy. Opcji nie jest dużo, jest ich ogrom! Oprócz funkcji, które dostępne są w innych oprogramowaniach, znajdziemy tu wiele unikalnych opcji, które zachwycą nawet osoby nie będące melomanami (jak choćby syntezator mowy do przechodzenia po menu bez patrzenia na ekran), ale i pozwolą na jeszcze większą swobodę dzięki wsparciu dla niemalże wszystkich istniejących formatów audio (a i nawet dla video!). Warto chociażby odpalić emulator, aby przekonać się o olbrzymiej ilości funkcji, nie oferowanej nigdzie indziej. Będąc przy temacie emulatora, jeśli planujecie zakup przenośnego odtwarzacza muzycznego, polecam zapoznać się z listą wspieranych urządzeń i przetestować, jak działa &quot;na sucho&quot;. A jak już mamy sprzęt na którym pójdzie Rockbox, wówczas wystarczy tylko zainstalować poprzez jedno kliknięcie przycisku. Prościej już nie może być.

Oczywiście Rockbox to nie tylko same plusy, zaleta w postaci mnogości opcji, jest też wadą. Na początku można zagubić się w gąszczu opcji, a interface w głębszych ustawieniach nie zawsze bywa domyślny. Trzeba się przyzwyczaić.

Twórcy na stronie udostępniają także potężną bazę wiedzy o dostępnych przenośnych odtwarzaczach. Parametry techniczne, porównania, opisy modułów, zdjęcia z rozkręcania urządzeń... ta wiedza jest na wyciągnięcie ręki i jest za darmo.

Uważam, iż warto spróbować Rockboxa i przekonać się o jego potędze. Czas poświęcony na zaznajomienie się z oprogramowaniem nie będzie zmarnowany, a zyskamy dzięki temu ogrom możliwości. Moja Sansa Clip+ od kiedy podarowałem jej Rockboxa, dostała jakby nowe życie. Gorąco polecam :)




## Edit - bateria na Rockboxie



Było kilka pytań odnośnie tego, jak bateria trzyma na nowym sofcie. Jeśli chodzi o Clip +, czas się wydłużył! Producent podaje max. czas w granicy 15h, zaś z Rockboxem, można osiągnąć nawet 17-18h.

Dla zainteresowanych zapraszam na stronę [http://www.rockbox.org/wiki/BatteryRuntime](http://www.rockbox.org/wiki/BatteryRuntime), gdzie podane są czasy pracy na baterii na różnych urządzeniach. Dodatkowo można zainstalować plugin do Rockboxa [http://www.rockbox.org/wiki/PluginBatteryBenchmark](http://www.rockbox.org/wiki/PluginBatteryBenchmark), który pomaga w przetestowaniu baterii i zebraniu statystyk. 