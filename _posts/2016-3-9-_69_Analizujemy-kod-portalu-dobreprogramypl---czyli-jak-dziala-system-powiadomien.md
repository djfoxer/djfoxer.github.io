---
layout:     post
title:      Analizujemy kod portalu dobreprogramy.pl — czyli jak działa system powiadomień
date:       2016-03-09 17:30:00
summary:    Ostatnim wpisem rozpoczął serię, która będzie opisywać zmagania z tworzeniem aplikacji do przechwytywania powiadomień z portalu dobreprogramy.pl w Windows 10 (+Mobile). Przyszedł zatem czas na coś konkretnego. Dziś przedstawię analizę, w jaki sposób na stronie zostało zrobione pobieranie powiadomień dla zalogowanego użytkownika. Z jednej strony będzie to dobrym wstępem do kolejnych wpisów i podwal...
categories: windows programowanie urządzenia mobilne
slug: Analizujemy-kod-portalu-dobreprogramy.pl-czyli-jak-dziala-system-powiadomien,71145.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307202637_0.PNG
---



Ostatnim wpisem rozpoczął serię, która będzie opisywać zmagania z tworzeniem aplikacji do przechwytywania powiadomień z portalu dobreprogramy.pl w Windows 10 (+Mobile). Przyszedł zatem czas na coś konkretnego. Dziś przedstawię analizę, w jaki sposób na stronie zostało zrobione pobieranie powiadomień dla zalogowanego użytkownika. 

Z jednej strony będzie to dobrym wstępem do kolejnych wpisów i podwaliny pod rozpoczęcie prac nad kodem, a z drugiej strony zapewne można będzie się  czegoś ciekawego dowiedzieć o aplikacjach web :)  (mam nadzieję :P )

Do dzieła! :)



> Nie będzie tutaj żadnej magii. Poniżej analizujemy jedynie i obserwujemy, jak działa system powiadomień od strony przeglądarki. Bez ingerencji w kod portalu.
 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307202637_0.PNG)





## F12 - zaczynamy analizę!



Pracę rozpoczniemy standardowo, jak zawsze kiedy zabieramy się za  *bałagan*  po stronie  frontendu, czyli od narzędzi deweloperskich w przeglądarce. Akurat z racji używania na co dzień Chroma, będzie to standardowe narzędzie dla programistów, dostępne zawsze pod klawiszem F12.





## Gdzie na stronie są powiadomienia?

 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307202642_0.png)



Na początku można wywnioskować, że powiadomienia są przesyłane jedynie na początku, przy ładowaniu strony. Zalogowany użytkownik dostaje wygenerowaną stronę, a w niej zawarty już kod HTML, który reprezentuje jego  *Centrum akcji* . 


Na szczęście tak nie jest, dzięki czemu zostaliśmy uchronieni przed parsowaniem kodu HTML za pomocą zewnętrznych bibliotek (takich jak np. HtmlAgilityPack).

Otóż,  *niedawno* , całkiem przypadkiem, odkryłem że powiadomienia z portalu są  *dynamicznie*  pobierane. Zobaczymy to po przejściu na zakładkę  *Network* , w narzędziach deweloperskich w Chrome. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307202641_0.PNG)



W celu łatwiejszego odnalezienia szukanego serwisu, przefiltrujmy wyniki klikając na opcję XHR. Pozwoli to nam na wydzielenie jedynie wysyłanych zapytań na serwer.

Po chwili zobaczymy, że co ok. 12 sekund wysyłany jest request.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307204259_0.PNG)



 *Strona*  wysyła zapytania na serwer pod adres (śmiało klikajcie!):



```html

http://www.dobreprogramy.pl/Providers/NotifyHelper.ashx?ping=ping&_=znacznik_czasu

```



Gdzie znacznik czasu jest inkrementowaną datą wejścia na stronę w postaci milisekund. Możemy łatwo to sprawdzić wpisując w konsoli JS:



```javascript

> new Date(1457379954093)
< Mon Mar 07 2016 20:45:54 GMT+0100 (Środkowoeuropejski czas stand.)

```



Mamy zatem już nasze źródło danych. Zobaczmy zatem co jest w środku.



## Zaglądamy do środka - lista powiadomień



Jeśli klikniemy w otwartej zakładce w narzędziu dev. na link, otrzymamy podgląd z otrzymanej wiadomości. Teraz po kliknięciu na zakładkę  *Preview*  ujrzymy sformatowany podgląd odpowiedzi z serwera. Eureka! :P 

 

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307205610_0.PNG)



Okazuje się, że co 12 sekund otrzymujemy JSONa z listą aktualnych powiadomień! Możecie sami sprawdzić swoje dane klikając nawet na powyższy link, poprzedniego akapitu.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307210334_0.PNG)


Otrzymane dane przechowywane są w liście  *current* , gdzie każdy element jest powiadomieniem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307210840_0.PNG)



Każdy z elementów posiada Id, a także link z grafiką (pole Avatar), dodatkowy tekst (CustomText), datę (Data), status (Status), adres URL (TargetUrl), tytuł (Title), typ powiadomienia (Type) i osobę odpowiedzialną za  *aktywację*  powiadomienia (UserName).

Co ciekawe, klucz w postaci: NUMER1:NUMER1 określa kolejno ID wpisu na blogu/aktualności/linku do programu, zaś drugi numer to ID powiadomienia. Przyda się nam to za chwilę.




## Zaglądamy do środka - akcje na liście



Zapewne zauważyliście, że można również oznaczać powiadomienia jako przeczytane i je usuwać:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307211521_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307211521_1.PNG)



Szybki podgląd w  *Networku*  wskazuje na to, że obie operacje są również wysyłane do tego samego  *serwisu*  (a dokładniej Handlera) NotifyHelper:





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307211809_0.PNG)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-9-_69_/g_-_-x-_-_-_x20160307211810_0.PNG)



Wówczas wysyłamy jedynie dodatkowy komunikat, to czy chcemy usunąć powiadomienie (deleteNotify), czy tylko oznaczyć jako przeczytane (markAsRead). Okazuje się zatem, że oprócz pobierania powiadomień, będziemy mogli je prosto usuwać i dezaktywować!



## Koniec?


Ufff. Dziś całkiem sporo udało się odsłonić z tego, jak działają powiadomienia na portalu, poprzez prostą analizę requestów w przeglądarce. Czy to zatem już koniec?

O nie :) To dopiero początek przygody :) Zostaje nam jeszcze jedno, chyba najważniejsze zagadnienie: skąd serwis wie, kto wysyła powiadomienia? Oczywiście wszystko znajduje się w przeglądarce użytkownika. Największym problemem będzie zatem dowiedzenie się co to jest i jak to wyłuskać, aby móc wysyłać i odbierać powiadomienia już nie z okna przeglądarki, ale z poziomu naszego własnego kodu. Te zagadnienie będę jednak starał się opisywać w kolejnych wpisach.

Zatem, do zobaczenia! :)


