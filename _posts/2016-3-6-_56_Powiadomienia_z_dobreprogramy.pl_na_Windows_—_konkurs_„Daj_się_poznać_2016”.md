---
layout:     post
title:      Powiadomienia z dobreprogramy.pl na Windows — konkurs „Daj się poznać 2016”
date:       2016-03-06 14:56:00
summary:    Na portalu dzieje się coraz więcej, a szczególnie teraz, gdy Redakcja uruchomiła swojego bloga, a także BugTrackera. Szczególnie ten ostatni jest interesującym eksperymentem, który wydaje się być świeżym podejściem do kontaktu z czytelnikami w polskim Internecie. W ten klimat idealnie wpisywać się b...
categories: windows programowanie urządzenia mobilne
---



Na portalu dzieje się coraz więcej, a szczególnie teraz, gdy Redakcja uruchomiła [swojego bloga](http://www.dobreprogramy.pl/BlogRedakcyjny), a także [BugTrackera](http://www.dobreprogramy.pl/BugTracker.html). Szczególnie ten ostatni jest interesującym eksperymentem, który wydaje się być świeżym podejściem do kontaktu z czytelnikami w polskim Internecie. 

W ten klimat idealnie wpisywać się będzie ciekawa inicjatywa, której będę uczestnikiem :)



## Daj się poznać - edycja 2016





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306133551_1.png)



Niedawno wystartował konkurs  [Daj się poznać](http://www.maciejaniserowicz.com/daj-sie-poznac/), a jego celem jest  *rozruszanie*   programistów, którzy prowadzą blogi. Każdy z uczestników musi założyć nowy (lub kontynuować już istniejący) projekt  open source i udostępnić go na GitHubie. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306133551_0.png)



Głównym celem nie jest stworzenie czegoś, co będzie wyjątkowe na skalę międzynarodową, a dzielenie się wiedzą i kodem z innymi. Stąd też prócz wrzucania kolejnych plików na GitHuba, ważnym elementem jest także tworzenie postów, które będą przedstawiały problemy i postęp prac nad zagadnieniem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306133552_0.png)



Pomimo, że konkurs już wystartował na dniach, nadal można zgłaszać się do niego do 13 marca. Zachęcam zatem osoby z naszego bloga do podjęcia wyzwania i spróbowania swoich sił w tej nietuzinkowej zabawie :)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306133553_0.png)



Prócz chwały i sławy można wygrać sporo ciekawych nagród, a także pozyskać nowych czytelników bloga. Po szczegóły odsyłam na stronę konkursu: [Daj się poznać](http://www.maciejaniserowicz.com/daj-sie-poznac/).


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306133554_0.png)






## Do dzieła! Zróbmy coś ciekawego!



Do konkursu zgłosiło się już ponad 200 osób i jest tam bardzo wiele ciekawych projektów, które mogą w przyszłości zaistnieć na większą skalę. Nie chcąc zostawiać w tyle, a przy okazji zmobilizować się do stworzenia czegoś ciekawego, również zgłosiłem się do konkursu. 



### DP Notification - powiadomienia z portalu wprost na Twój komputer i smartfon



Projekt, jaki zamierzam zrobić, będzie bezpośrednio związany z portalem dobreprogramy.pl. Otóż moim celem jest stworzenie uniwersalnej aplikacji na Windows 10 i Windows 10 Mobile (a zapewne także w późniejszych etapach portu na Androida i iOS), która będzie pozwalała na wyświetlanie powiadomień z portalu bezpośrednio na urządzeniu z Windowsem.

Zamiast wchodzić na stronę i klikać w ikonkę z powiadomieniami, w celu sprawdzenia nowych wiadomości, będziemy dostawali automatycznie komunikaty w pasku powiadomień. Myślę, że będzie to znacznie ciekawsza aplikacja, niż oficjalna, obecnie dostępne w Sklepie, która pozwala jedynie na komentowanie wpisów i przeglądanie treści portalu. 

Spróbujemy zatem przenieść te powiadomienia z www:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306143159_0.PNG)



Na system Windows 10 i Windows 10 Mobile (Android i iOS będzie zapewne później jako odnoga w tworzeniu aplikacji wieloplatformowych):



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306143204_0.PNG)





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-6-_56_/g_-_608x405_-_-_71094x20160306143449_0.png)



Aplikacja zostanie finalnie udostępniona w sklepie Microsoft jako apka uniwersalna. Źródła będę wrzucał na GitHuba [pod tym linkiem](https://github.com/djfoxer/dp.notification). Oczywiście kolejne walki z nową platformą uniwersalną i próbą  *zhackowania*  portalu :P  będę publikował na blogu.

Planują podzielić pracę na kilka etapów:


  * przygotowanie środowiska


  * stworzenie API w C#,  które będzie pozwalało na logowanie/wylogowanie i pobieranie nowych powiadomień z dobreprogramy.pl


  * wstępne zaprojektowanie interfejsu


  * stworzenie solucji do W10 i W10M, wykorzystującej powyższe API


  * otwarte testy


  * stworzenie finalnego mockupu ekranów


  * połączenie całości 


  * udostępnienie apki w Sklepie Windows 10 (Mobile)



Liczę również na ciekawe opinie i komentarze od czytelników bloga i portalu dobreprogramy.pl. Będę niezmiernie wdzięczny za wszelkie podpowiedzi, uwagi, a także pochwały i nagany ;) 


Mam nadzieję, że zaproponowany przeze moją osobę  projekt na konkurs okaże się finalnie ciekawym pomysłem. W najbliższych dniach rozpocznę już pracę nad apką i kolejne wpisy będą już związane z omawianym zadaniem konkursowym. Liczę na to, że uniwersalna apka do powiadomień dla użytkowników portalu będzie ciekawym dodatkiem nie tylko dla wiernych czytelników/blogerów, ale i dla zwykłych osób posiadających konta na portalu.
