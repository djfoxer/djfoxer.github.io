---
layout:     post
title:      DobryBackupBloga —  aplikacja do szybkiej archiwizacji wpisów blogowych
date:       2017-09-15 11:28:00
summary:    Nowy blog zbliża się wielkimi krokami. Zapewne w październiku będziemy cieszyli się zarówno nowymi blogami, jaki i aplikacją mobilną, a może również odświeżeniem portalu.Z tego co zapowiada Lisek blog przejdzie gruntowny remont, łączenie z nowym formatem wpisów blogowych (zniknie bbcode). Może to właśnie dobry moment, aby każdy bloger zbackupował własne wpisy z bloga. Oczywiście ręczne kopiowanie ...
categories: oprogramowanie internet hobby
slug: DobryBackupBloga--aplikacja-do-szybkiej-archiwizacji-wpisow-blogowych,83137.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-9-15-_14_/g_-_-x-_-_-_x20170915094722_0.png
---



Nowy blog zbliża się wielkimi krokami. Zapewne w październiku będziemy cieszyli się zarówno nowymi blogami, jaki i aplikacją mobilną, a może również odświeżeniem portalu.

Z tego co zapowiada Lisek blog przejdzie gruntowny remont, łączenie z nowym formatem wpisów blogowych (zniknie bbcode). Może to właśnie dobry moment, aby każdy bloger zbackupował własne wpisy z bloga. Oczywiście ręczne kopiowanie wpisów i pojedynczych grafik nie ma sensu (ja mam ich 200!). Stąd też na potrzebę tego zadania napisałem aplikację do backupowania wpisów blogowych i tak powstał...







## DobryBackupBloga


Aplikacja przeznaczona jest dla osób posiadających blog na portalu dobreprogramy.pl. Służy ona do archiwizacji wpisów blogowych na lokalnym dysku użytkownika. Przenoszone są wszystkie opublikowane wpisy blogera wraz z grafikami.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-9-15-_14_/g_-_-x-_-_-_x20170915094722_0.png)





> Link do pobrania: [dobryBackupBloga](http://foxersoft.com/dobryBackupBloga.zip)




### Konfiguracja



Konfiguracja programu jest bardzo prosta. Wystarczy w dołączonym pliku do aplikacji  *cfg.cfg*  uzupełnić następujące parametry:



```cpp

login
password
imgUlrNewPrefix
blogUlrOldPrefix [opcjonalne]
blogUlrNewPrefix [opcjonalne]

```



login - login użytkownika,

hasło - hasło użytkownika,

imgUlrNewPrefix - nowy prefix do grafik, podmienia w tagach adresy grafik z bloga, np.  *https://gallery.dpcdn.pl/imgc/UGC/83137/g_-_-x-_-_-_83137x20170915094722_0.png*  na  *https://mojbackup.oj.tam/img/g_-_-x-_-_-_83137x20170915094722_0.png* 

blogUlrOldPrefix - prefix do aktualnego adresu bloga (u mnie jest to https://www.dobreprogramy.pl/djfoxer/), 

blogUlrNewPrefix - nowy prefix do wpisów,  pozwala to na przeniesienie odnośników we wpisach, np. we wpisie odnośnik  *https://www.dobreprogramy.pl/djfoxer/Bad-Word-Detector--wlasna-wtyczka-do-detekcji-wulgaryzmow-w-Visual-Studio,81299.html*  zostanie podmieniony na  *https://mojbackup.oj.tam/Bad-Word-Detector--wlasna-wtyczka-do-detekcji-wulgaryzmow-w-Visual-Studio,81299.html* 

Przy uruchomieniu pojawią się zaczytane parametry:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-9-15-_14_/g_-_-x-_-_-_x20170915101116_0.PNG)



jeśli dane do logowania będą się zgadzać, aplikacja przystąpi do robienia backupu:




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-9-15-_14_/g_-_-x-_-_-_x20170915101116_1.PNG)





### Pliki backupu - szczegóły


Po wykonaniu operacji backup zostanie zapisany w folderze  *blogs* , w miejscu z którego uruchomiliśmy program do backupu.

Każdy wpis blogowy będzie posiadał pojedynczy plik tekstowy z wpisem, a także folder, w którym znajdą się grafiki z danego wpisu.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-9-15-_14_/g_-_-x-_-_-_x20170915101944_0.PNG)



Dodatkowo każdy z wpisów na początku otrzymuje labelkę z informacjami o wpisie

---
layout:     post
title:      tytuł wpisu
date:       data wpisu
summary:    opis, pierwsze 400 znaków z wpisu
categories: wybrane kategorie/tematy sparsowane z konfiguracji wpisu
slug: adres wpisu np. https://www.dobreprogramy.pl/djfoxer/Realtek-HD-Audio-rozwiazanie-problemow-z-nagrywaniem-przez-mikrofon-i-kilka-dygresji,17467.html
---

Z racji tego, iż format wpisów będzie i tak zmieniany, pliku backupu mają znaczniki markdown. Podmianie objęte są znaczniki h2=> ##, h3 => ###, i => *tekst*, list/numlist => [usunięcie, zostanie tylko item jako *, czyli standardowe wypunktowanie], item => *, url => [opis](url), code => ```, quote => >, img/image => ![desk](adres)




### Znane błędy


Problemy mogą pojawić się przy generowaniu prawidłowych adresów url do wpisów i zdjęć u osób, które nie aktywowały w konfiguracji bloga aliasu. Aplikację testowałem na swoim koncie i działa ona wyśmienicie. Mogą jednak pojawić się problemy w szczególnych przypadkach. Niestety bez dostępu do kont, na jakich to się dzieje, nie będę w stanie naprawić tych problemów.

Mam nadzieję, że aplikacja przyda się wam i liczę na komentarze oraz sugestie. 
