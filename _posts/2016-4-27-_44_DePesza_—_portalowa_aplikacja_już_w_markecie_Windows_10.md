---
layout:     post
title:      DePesza — portalowa aplikacja już w markecie Windows 10
date:       2016-04-27 18:38:00
summary:    Nastał ten dzień i portalowa aplikacja DePesza zawitała do sklepu Windows 10.Zapraszam chętnych do zainstalowania aplikacji na systemie Windows 10, zarówno na desktopie, jak i na urządzeniu mobilnym.DePesza w markecie Windows 10 i Windows 10 Mobile: linkWersja alfa — co oferuje?Nie ukrywam, że obecn...
categories: windows programowanie urządzenia mobilne
---



Nastał ten dzień i portalowa aplikacja DePesza zawitała do sklepu Windows 10.
Zapraszam chętnych do zainstalowania aplikacji na systemie Windows 10, zarówno na desktopie, jak i na urządzeniu mobilnym.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160426233227_0.png)



<blockquote>
<p>DePesza w markecie Windows 10 i Windows 10 Mobile: [link](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2)</p>
</blockquote>




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160427002725_0.PNG)





## Wersja alfa — co oferuje?



Nie ukrywam, że obecna wersja w markecie jest jeszcze wczesną wersją alfa, która posiada zapewne  wiele błędów i niedoróbek. Jednakże już teraz można się zalogować w celu rozpoczęcia pracy z DePeszą i zarządzać w podstawom stopniu powiadomieniami z portalu.

Aplikacja obecnie oferuje swoim użytkownikom:


  * bezpieczne logowanie/wylogowanie


  * brak przetrzymywania hasła użytkownika


  * pobieranie listy powiadomień z portalu (odpowiednie wyświetlanie)


  * pobieranie powiadomień w trakcie pracy aplikacji (co 30 sekund)


  * pobieranie powiadomień, gdy aplikacja jest wyłączona (co 15 minut)


  * wyświetlanie graficznego okienka, gdy w pobranych powiadomieniach z portalu otrzymamy nową notyfikację


  * możliwość przejścia do linku związanego z powiadomieniem po kliknięciu na nową wiadomość na liście/graficznym okienku


  * automatyczne oznaczanie przeczytanych powiadomień i ich późniejsze usuwanie


  * całkowite usunięcie przeczytanych powiadomień


  * przechowywanie powiadomień zalogowanego użytkownika





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160427001509_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160427001510_0.png)






## Bezpieczeństwo



Zapewne bardzo ważną kwestią jest bezpieczeństwo przechowywania danych. DePesza na żadnym etapie nie przechowuje hasła użytkownika. Jedynie co jest zapisywane to informacja kto się zalogował (login), czas logowania i data wygaśnięcia ciasteczka. Samo ciasteczko nie jest również nigdzie w kodzie zapisywane , a jedynie trzymanie w systemowej sesji przeglądarki aplikacji. Zapewnia to bezpieczeństwo i brak obawy o niepowołany dostęp do wrażliwych danych użytkownika.

<blockquote>
<p>DePesza na żadnym etapie nie przechowuje hasła użytkownika</p>
</blockquote>



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160426233726_0.png)





## Early access — wiele zmian przed nami



Obecna wersja został opublikowana w wersji dość wczesnej, ale pozwalającej już na codzienną pracę z aplikacją. Podstawowe operacje na powiadomieniach są dostępne i nie powinny generować problemów.

W przyszłych wersjach skupię się na kolejnych funkcjonalnościach, które zostaną dodane do aplikacji. Oczywiście już teraz widzę wiele pomniejszych błędów i niedociągnięć, które należy jak najszybciej wyeliminować. Także sam kod wymaga refactoringu i uporządkowania, aby łatwiej w przyszłości naprawiać, modyfikować i dodawać kolejne elementy do DePeszy.

Od strony UI aplikacja wymaga również dopieszczenia, a obecna szata graficzna ma być funkcjonalna. Na wodotryski w interfejsie jeszcze przyjdzie pora i nie jest to obecnie najwyższym priorytetem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160426233102_0.jpg)





## Co dalej — plan na kolejne iteracje



W wolnej chwili będę skupiał się na doszlifowaniu aplikacji pod kątem:


  * ujednolicenie wyświetlanych komunikatów o nowych notyfikacjach


  * wyeliminowanie skoku przy odświeżaniu listy


  * wykorzystanie współdzielonych danych w chmurze do przechowywania informacji o odebranych powiadomieniach


  * dodanie gestów do usuwania/oznaczania powiadomień na liście


  * dopieszczenie interfejsu




Oczywiście priorytetem jest naprawa błędów, krytycznych ścieżek w aplikacji i ciągły refactoring poprawiający jakość i czytelność kodu.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160426234036_0.png)





## Zgłaszanie błędów i propozycji


Mam nadzieję, że po instalacji nie zrazicie się do aplikacji :) Zapewne posiada ona wiele bugów, ale liczę na waszą pomoc. Jeśli zauważycie jakieś błędy, może macie jakieś propozycje od strony funkcjonalności, interfejsu, może loga lub propozycje w głębi samej apki - to zapraszam do zgłaszania tego typu uwag. Można to robić oczywiście w komentarzach, ale proszę aby finalnie taka informacja została zgłoszona na oficjalnej stronie, do tego przeznaczonej.

W celu zgłoszenia buga, zaproponowania zmian itp. itd. proszę o dodawania zgłoszeń na stronie [https://github.com/djfoxer/dp.notification/issues](https://github.com/djfoxer/dp.notification/issues)

<blockquote>
<p>Bugi i propozycje proszę zgłaszać na stronie: [link](https://github.com/djfoxer/dp.notification/issues)</p>
</blockquote>



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160426233527_0.jpg)




Zapraszam zatem do testowania i zgłaszania uwag. Kolejne wersje aplikacji będą wychodziły w zależności od ilości zgłoszeń i zainteresowania użytkowników DePeszą, a także od ilości wolnego czasu u mojej skromnej osoby ;)


<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-27-_44_/g_-_608x405_-_-_72628x20160426232640_0.png)



