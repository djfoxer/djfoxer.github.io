---
layout:     post
title:      Aktualizujemy aplikację w nowym Windows DevCenter
date:       2016-05-31 23:38:00
summary:    Wydanie aktualizacji aplikacji to spore wydarzenie dla każdego dewelopera. Niezliczone ilości godzin przesiedziane przed monitorem, kartką z notatkami, rozmowami z klientami czy testami w końcu mogą zaowocować stworzeniem poprawionej, nowej wersji oprogramowania.Wychodzę z założenia, że proces pierw...
categories: windows oprogramowanie programowanie
---



Wydanie aktualizacji aplikacji to spore wydarzenie dla każdego dewelopera. Niezliczone ilości godzin przesiedziane przed monitorem, kartką z notatkami, rozmowami z klientami czy testami w końcu mogą zaowocować stworzeniem poprawionej, nowej wersji oprogramowania.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_38_/g_-_608x405_-_-_73640x20160531232056_0.jpg)



Wychodzę z założenia, że proces pierwszej certyfikacji macie już za sobą i dziewicza wersja dostępna jest już w markecie.

Tworząc kolejne odsłony aplikacji na Universal Windows Platform, natknąć się można na pewne problemy i niejasności przy aktualizacji naszego programu poprzez DevCenter. Dodatkowo Microsoft niedawno wydał odświeżoną wersję testową [centrum developerskiego](https://developer.microsoft.com/en-us/dashboard/apps/overview), która doczekała się kilu nowości i ułatwień. 

Zatem jak tego dokonać? Na co uważać? 

Proces aktualizacji na początku wydaje się skomplikowany, ale szybko można się oswoić z tym zadaniem. Oto kilka porad, o czym pamiętać przy wypuszczaniu nowej wersji do marketu. Oczywiście przydadzą się one również w przypadku dodawanie pierwszej wersji aplikacji.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_38_/g_-_608x405_-_-_73640x20160601020510_0.PNG)





  * Aktualizacji dokonujemy na zakładce  *Submissions*  poprzez przycisk  *Update* 
na wersji, która jest już w markecie.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_38_/g_-_608x405_-_-_73640x20160601014744_0.PNG)


Wówczas po udanej certyfikacji nowa wersja zastąpi starszą.



  * Rozpoczęcie aktualizacji nie wycofuje i nie zmienia niczego w obecnie dostępnym wydaniu. Dopiero kliknięcie na przycisk  *Submit to the Store*  zablokuje zmiany i rozpocznie proces certyfikacji. 


  * Podczas certyfikacji w każdej chwili można zaprzestać tego procesu, a także całkowicie usunąć aktualizację.


  * Pamiętaj, aby podać w opisie co wnosi nowa wersja ( *App description -> Release notes* ). Wydaje się to logiczne, ale sam Microsoft o tym zapomina i wypuszcza aktualizacje swoich apek bez tej informacji!


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_38_/g_-_608x405_-_-_73640x20160531232530_0.PNG)





  * System, po dodaniu nowej wersji paczki, wyświetli komunikat, który porówna paczkę z aktualizacją, z jej obecną wersją w markecie. Szybko odnajdziemy, jakie systemy będą wspierane po certyfikacji.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_38_/g_-_608x405_-_-_73640x20160601021144_0.PNG)


 


  * Warto zweryfikować czy kryteria wiekowe nie powinny zostać zmienione (często niewinna opcja, jak np. pobieranie danych z sieci, nad którymi nie mamy wpływu, jak zdjęcia, mogą wymuszać podniesienie minimalnego wieku)


  * Jeśli dodamy nowy język w projekcie w Visual Studio to pamiętajmy o tym, że będzie on automatycznie wykryty jako kolejne pola do uzupełniania opisu. 


  *  *Notes for certification*  to bardzo ważna zakładka, to tam przesyłamy informacje do testera naszego programu (jak. np. testowy login i hasło do aplikacji, bez których nie zalogujemy się do apki). W tym miejscu możemy poinformować osobę o zmianach dokonanych przez nas, jakie były wymagane w celu poprawnej finalizacji certyfikacji (np. aktualizacja licencji w języku obcym dla testera)


  * Sam proces certyfikacji aktualizacji jest zawsze szybszy niż za pierwszym razem. Zależy to jednak też od ilości dokonanych zmian 


  * Po pomyślnej certyfikacji jeszcze przez kilka godzin w markecie może być dostępna starsza wersja aplikacji 



Mam nadzieję, że taki szybki poradnik przyda się osobom, które rozpoczynają swoją przygodę z Windows Dev Center. 



<blockquote>
<p>DePesza dostępna jest w markecie Windows 10 (desktop i mobile). Bezpośredni link: [DePesza](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2).</p>
</blockquote>

<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_38_/g_-_608x405_-_-_73640x20160601013916_0.png)


