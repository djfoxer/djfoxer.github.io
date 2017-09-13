---
layout:     post
title:      Analiza logowania do portalu dobreprogramy.pl — uzyskujemy dostęp do zasobów użytkownika
date:       2016-03-12 12:23:00
summary:    Za nami już wpis odnośnie sposobu działania systemu powiadomień na portalu. Przed przystąpieniem do tworzenia kodu należy koniecznie przeanalizować jeszcze jeden, najważniejszy element tego zagadnienia - logowanie do portalu.System powiadomień, opisany wcześniej, działa na podstawie zalogowanego uży...
categories: windows programowanie urządzenia mobilne
---



Za nami już wpis odnośnie sposobu działania [systemu powiadomień](http://www.dobreprogramy.pl/djfoxer/Analizujemy-kod-portalu-dobreprogramy.pl-czyli-jak-dziala-system-powiadomien,71145.html) na portalu. Przed przystąpieniem do tworzenia kodu należy koniecznie przeanalizować jeszcze jeden, najważniejszy element tego zagadnienia - logowanie do portalu.

System powiadomień, opisany wcześniej, działa na podstawie zalogowanego użytkownika, czyli na podstawie ciasteczka przechowywanego w przeglądarce klienta. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160312114936_0.png)









## Mieć ciastko i zjeść ciastko



Ponownie do pracy niezbędne będzie nam narzędzie deweloperskie, dostarczone wraz z przeglądarką. Zaczniemy od ciasteczka. Kiedy użytkownika podłączy się do aplikacji ASP.NET generowana jest sesja, która identyfikowana jest po unikalnym kluczu. &#211;w klucz zwracany jest dla użytkownika i przechowywany w ciasteczku w przeglądarce. Aplikacja ASP.NET wrzuca klucz w ciasteczko o nazwie:  *ASP.NET_SessionId* . 

Sesja tworzona jest już przy podłączeniu do aplikacji webowej, zatem już przed zalogowaniem otrzymujemy id sesji. Własne ciasteczko możemy podejrzeć w narzędziu deweloperskim, wchodząc na zakładkę  *Resources*  i klikając na  *Cookies -&gt; www.dobreprogramy.pl* :



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160310191930_0.PNG)





## Logowanie na dwa sposoby



Najciekawsze jest tutaj to, że portal posiada dwa, zupełnie różne sposoby na zalogowanie się. Do pierwszego dostaniemy się przez odrębny link, który pojawia się gdy zechcemy zalogować się z  *podstron*  (np. logowanie z poziomu bloga). Możemy do niej przejść także poprzez szybkie kliknięcie w przycisk  *logowanie*  na stronie głównej, zanim nie załadują się wszystkie skrypty na stronie. Drugi sposób pojawia się jako domyślna opcja logowanie, po pełnym pobraniu strony głównej.

Poniżej omówię dwie ścieżki, a na koniec opisze, który sposób będzie używany w naszej aplikacji do logowania i dlaczego. Zatem zacznijmy od:




## Logowanie sposób nr 1 - dedykowana strona, klasyczny formularz



Głowna strona do logowania znajduje się pod adresem:


```html
https://ssl.dobreprogramy.pl/Logowanie.html
```




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160310182056_0.PNG)



Dostaniemy się do niej  przez link. Jest to klasyczny formularz. Zatem wpisujemy swoje dane do logowania i załóżmy, że  dodatkowo zaznaczamy opcję &quot;W przyszłości zaloguj mnie automatycznie&quot;, dzięki niej będziemy zawsze zalogowani.

Załóżmy, że wpisaliśmy swoje dane i kliknęliśmy na przycisk logowania. Przejdźmy teraz na zakładkę  *Network* , aby podejrzeć co się dzieje podczas logowania do portalu (warto zaznaczyć opcję  *Preserve log* , aby przeglądarka nie czyściła logów przy przeładowaniu):



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160311172648_0.png)



Jak na dłoni widzimy przesłany login i hasło oraz opcję automatycznego logowania. W zapytaniu zauważymy również ciasteczko, które otrzymaliśmy przy pierwszym wejściu na stronę, a także komplet danych charakterystycznych dla aplikacji ASP.NET (ViewState). Widzimy tutaj element  *EVENTTARGET* , który informuję jaka kontrolka (ID) wywołuję akcję, w tym przypadku jest to  *link*  do logowania ( *lnkLogin* ).

 *Po zalogowaniu dostajemy inne (nowe) ciasteczko ( *ASP.NET_SessionId* ) niż te, którym się logowaliśmy.*  



## Logowanie sposób nr 2 - dedykowany  *serwis* , łatwiejsze wykorzystanie



Drugim sposobem na logowanie jest wyskakujące  *okienko* . Od strony klienta funkcjonalnie nie różni się ono niczym od dedykowanej strony, prócz oczywiście tym, że nie przechodzimy na oddzielną podstronę, a po zalogowaniu strona sama się odświeży 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160311180643_1.PNG)



Kolejny raz po odpaleniu narzędzi deweloperskich zaglądamy, jak wygląda mechanizm logowania. Tutaj sprawa jest znacznie prostsza. W tym miejscu system logowana korzysta z handlera ASP.NET znajdującego się pod adresem:


```html
https://ssl.dobreprogramy.pl/Providers/LoginProvider.ashx
```




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160311180700_0.png)



Widzimy, że w tym przypadku również przekazujemy oczywiście login, hasło, ciasteczko i opcję automatycznego logowania. Ważnym elementem wysyłanych danych jest parametr  *what* , który określa akcję, w tym przypadku jest to logowanie ( *login* ).

Co ciekawe, ten sposób logowania nie zwraca nowego ciasteczka, jak miało to miejsce  wcześniej.  *Po zalogowaniu zostajemy z tym samym ciasteczkiem (ASP.NET_SessionId), jakim się logowaliśmy.* 




## Jak będziemy się logowali w tworzonej aplikacji W10 (+Mobile)?



Wybór jest oczywisty. Tworząc już w C# bardzo prosty  *proof of concept*  sprawdziłem, iż metoda druga jest znacznie prostsza do implementacji i wymaga mniej przesyłanych danych. Nie musimy przekazywać informacji, które trzeba byłoby wyłuskać z kodu HTML za pomocą dodatków, jak chociażby  HtmlAgilityPack. Jest ona bardzo podobno do sposobu, w jaki zrobiony jest mechanizm do zarządzania powiadomieniami. 

Logowanie opierać będzie się na następującym schemacie:


  * Wysłanie z poziomu kodu zapytania do strony w celu pobrania ciasteczka z odpowiedzi (zapewne będzie klasyczna to strona do logowania, która niewiele waży) 


  * Wysłanie poprawnie stworzonego zapytania do handlera  *LoginProvider*    


  * [Tu nastąpi logowanie na serwerze]


  * Będziemy mogli już jako zalogowany użytkownik zarządzać powiadomienia z portalu poprzez handler   *NotifyHelper*  (do zapytania  *doklejone*  zostanie ciasteczko)


  * Tadammm!! :P





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-12-_54_/g_-_608x405_-_-_71265x20160312112733_0.png)





## Co dalej: czas na tworzenie kodu - logowanie


Jest to już ostatni wprowadzający wpis w serii, który przedstawia działanie podstawowych elementów portalu dobreprogramy. 

W kolejnym poście rozpoczniemy już tworzenie aplikacji. Prócz bardzo podstawowego wprowadzenia do środowiska pracy i solucji będzie już konkretny kod, który powyższą analizę przeleje na C# i pozwoli na zalogowanie się do portalu z poziomu .NET. Oczywiście kod będzie wrzucany regularnie na [GitHuba](https://github.com/djfoxer/dp.notification), zapewne trochę wcześniej niż będzie publikowany wpis.

Zapraszam zatem już teraz do kolejnych części serii.
