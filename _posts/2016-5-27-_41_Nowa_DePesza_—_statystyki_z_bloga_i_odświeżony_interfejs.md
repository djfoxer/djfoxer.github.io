---
layout:     post
title:      Nowa DePesza — statystyki z bloga i odświeżony interfejs
date:       2016-05-27 18:11:00
summary:    W niedawnym wpisie odnośnie pierwszej aktualizacji dostałem bardzo dużo ciekawych uwag i pomysłów, jak ulepszyć kilka elementów w DePeszy. Przyznaję, że wiele z nich było bardzo twórczych i skłoniło mnie do poświecenia kilku wieczorów na doszlifowanie aplikacji. Ciesze się, że DePesza zyskała spore ...
categories: windows programowanie urządzenia mobilne
---



W niedawnym wpisie odnośnie [pierwszej aktualizacji](http://www.dobreprogramy.pl/djfoxer/DePesza-aktualizacja-i-nowe-pomysly,72802.html) dostałem bardzo dużo ciekawych uwag i pomysłów, jak ulepszyć kilka elementów w DePeszy. Przyznaję, że wiele z nich było bardzo twórczych i skłoniło mnie do poświecenia kilku wieczorów na doszlifowanie aplikacji. Ciesze się, że DePesza zyskała spore grono zainteresowanych osób chętnych do testów i dzielenia się pomysłami. Obecne wydanie jest już stabilnym i przyjemnym dla oka programem. Dziękuję również wszystkim za wnikliwe testy i podesłane uwagi ([mordzio](http://www.dobreprogramy.pl/mordzio), [PAMPKIN](http://www.dobreprogramy.pl/PAMPKIN), [AntyHaker](http://www.dobreprogramy.pl/AntyHaker), [Berion](http://www.dobreprogramy.pl/Berion), [tylko_prawda](http://www.dobreprogramy.pl/441441,tylko_prawda,Uzytkownik.html)).

Od kilkudziesięciu godzin w markecie dostępna jest druga aktualizacja do DePeszy.

<blockquote>
<p>DePesza dostępna jest w markecie Windows 10 (desktop i mobile). Bezpośredni link: [DePesza](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2).</p>
</blockquote>

Poniżej przedstawię zmiany, jakie zostały wprowadzone w tym wydaniu. Jest ich całkiem sporo i myślę, że zadowolą one użytkowników portalu z systemem Windows.

<blockquote>
<p>Po aktualizacji jeśli statystyki nie pokazują nic lub nie masz nowych powiadomień  *spróbuj się przelogować* !</p>
</blockquote> 



## Nowe logo


Najbardziej rzucającą się w oczy zmianą jest odświeżone logo. Po przedostatniej publikacji o zmianach w DePeszy zgłosił się do mnie Jarek Uliczka. Zaproponował stworzenie nowego loga do aplikacji, które bardziej pasowałoby do charakteru programu. Przyznaję, że wynikowa praca bardzo pozytywnie mnie zaskoczyła i cieszę się z tej owocnej współpracy, za co dziękuję :) 

Efekt finalny jest niezmiernie udany:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182204_0.jpg)





## Statystyki do bloga


Nowa funkcjonalność, która zapewne przypadnie do gustu blogerom z portalu są statystyki. Pomysł podrzucił użytkownik [mordzio](http://www.dobreprogramy.pl/mordzio). W dolnym menu na liście kontaktów znajduje się przycisk  *statystyki*  (ikonka kalkulatora). Przenosi on do podstrony, gdzie można uruchomić analizę, która zbierze wszystkie wpisy blogowe zalogowanej osoby.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182202_1.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182206_0.png)



Znajdziecie tutaj pełną listę wpisów z bloga, a także informacje o ilości wyświetleń i komentarzy oraz liczbę wpisów na głównej stronie. Publikacje można sortować po dacie wprowadzenia, wyświetleniach i komentarzach. Szybko odnajdziecie najchętniej czytane i komentowane pozycje, a także globalne statystyki odnośnie swojego bloga. 

Szczegóły odnośnie uzyskiwania danych (HTML Agility Pack) opisałem w [ostatnim wpisie](http://www.dobreprogramy.pl/djfoxer/Html-Agility-Pack-uzyskujemy-statystyki-z-bloga-do-DePeszy-czyli-parsujemy-HTML-w-C,73386.html).



## Odświeżona lista z powiadomieniami


Sporo pomysłów podrzucił także [Berion](http://www.dobreprogramy.pl/Berion). Jednym z nich było lepsze wydzielenie notyfikacji na liście. Finalnie zdecydowałem się na lekką przezroczystość z białym tłem, aby uwidocznić poszczególne elementy. Dorzuciłem również animacje, które pojawiają się przy dodawaniu i usuwaniu pozycji z listy. Sama tabelka z powiadomieniami przestała także migać, w przypadku odświeżenia danych.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182201_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182205_0.png)



Same tło również zostało rozmyte, aby nie odciągało wzroku od głównego elementu - powiadomień.



## Okrągłe awatary

 
Kolejna nowość zasugerowana przez [Berion](http://www.dobreprogramy.pl/Berion) to użycie okrągłych awatarów, zamiast ich kwadratowych odpowiedników. Taka zmiana bardziej wpasowuje się z styl Windows 10. Awatary zostały zaokrąglone na liście notyfikacji, jak i w wyskakujących powiadomieniach. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525230356_0.png)





## Zielone ramki


Małym problemem, ale psującym jednak odbiór całości były, szare ramki okna w Windows 10. Zamieniłem je na zielone, z białym napisem, tak, aby pasowały bardziej do koloru przewodniego aplikacji.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525230901_0.png)





## Nowy pasek menu


Do poprawki poszedł także dolny pasek z menu. Obecnie ikony znajdują się po prawej stronie i są domyślnie zwinięte. Doszły również nowe pozycje:  przejście do podstrony ze statystykami i ikona otwierająca okno z informacjami o aplikacji. 

 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525231302_0.png)





## Przejście do kolejnego elementu po Enterze


Użytkownik [kilijanek](http://www.dobreprogramy.pl/kilijanek) słusznie zauważył, że przydałoby się również przejście do kolejnych pól podczas logowania poprzez klawisz Enter. Mała rzecz, a o ile przyspiesza proces logowania. Teraz będąc w polu  *login*  i klikając na Enter przejdziemy do pola  *hasło* . Z  tego miejsca poprzez klawisz Enter rozpoczniemy proces logowania, bez potrzeby klikania ręcznie na przycisk * Zaloguj się* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182204_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182204_1.png)





## Menu na powiadomieniu


Na ten czas zdecydowałem się na zmianę w zarządzania pojedynczym powiadomieniem. Teraz klikając na element na liście otrzymamy menu z wyborem opcji do wybranej notyfikacji:



  * Otwórz link (ustawia jednocześnie status na przeczytany)


  * Ustaw jako przeczytany (tylko w nowych)


  * Usuń






![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182202_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525182208_1.png)





## Domyślny dźwięk powiadomienia

 
Wiele osób narzekało na domyślny dźwięk powiadomienia, który był dość  *specyficzny*  ;) Aby nikogo nie uszczęśliwiać na siłę, zmieniłem go na standardowy dźwięk systemowy. Jeśli ktoś będzie chciał ustawić inny, może oczywiście zrobić to z ustawień systemowych.



## Kolejny krok - Xamarin


Mam nadzieję, że nowe zmiany zadowolą użytkowników. Wydaj się, że obecna wersja na Windows 10 i Mobile jest już całkiem ustabilizowana. W niedługim czasie rozpocznę szykowanie się do stworzenia wersji na Androida i iOS. Przygotowywać się będę z Pluralsightem. Mam nadzieję, że praca z Xamarinem pod Visual Studio nie okaże się multiplatformową udręką :)  

Oczywiście nadal czekam na kolejne uwagi i ciekawe propozycje, a także na słowa otuchy i wirtualne  *poklepywanie po pleckach*  :P 


<blockquote>
<p>Kod aplikacji jest otwarty, a aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-27-_41_/g_-_608x405_-_-_73499x20160525225603_0.png)




