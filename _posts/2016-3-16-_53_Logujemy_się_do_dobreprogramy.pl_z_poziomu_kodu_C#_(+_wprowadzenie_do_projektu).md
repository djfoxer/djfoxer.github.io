---
layout:     post
title:      Logujemy się do dobreprogramy.pl z poziomu kodu C# (+ wprowadzenie do projektu)
date:       2016-03-16 18:12:00
summary:    Dwa ostatnie wpisy przedstawiały analizę sposobu logowania się i zarządzania powiadomieniami na portalu dobreprogramy. Przyszedł już czas na stworzenie kodu w C#, który pozwałaby już coś w praktyce zrobić.Dzisiaj skupimy się na logowaniu do portalu, a zapewne na dniach przedstawię mechanizm do zarzą...
categories: windows programowanie urządzenia mobilne
---



Dwa ostatnie wpisy przedstawiały analizę sposobu [logowania się](http://www.dobreprogramy.pl/djfoxer/Analiza-logowania-do-portalu-dobreprogramy.pl-uzyskujemy-dostep-do-zasobow-uzytkownika,71265.html) i [zarządzania powiadomieniami](http://www.dobreprogramy.pl/djfoxer/Analizujemy-kod-portalu-dobreprogramy.pl-czyli-jak-dziala-system-powiadomien,71145.html) na portalu dobreprogramy. Przyszedł już czas na stworzenie kodu w C#, który pozwałaby już coś w praktyce zrobić.

Dzisiaj skupimy się na logowaniu do portalu, a zapewne na dniach przedstawię mechanizm do zarządzania powiadomieniami. 

Na początku jednak mały wstęp odnośnie samego projektu.



## Szkielet aplikacji

 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-16-_53_/g_-_608x405_-_-_71411x20160315224532_0.png)



Aplikacja tworzona będzie w Visual Studio 2015 Community (wersja pozwala na działania komercyjne, zupełnie za darmo, szczegóły licencji [tutaj](https://www.visualstudio.com/support/legal/mt171547)).



Projektem naszym jest oczywiście aplikacja uniwersalna - Universal Windows. Pozwala ona na tworzenie oprogramowania zarówno pod Windows 10, jak i Winodows 10 Mobile.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-16-_53_/g_-_608x405_-_-_71411x20160315224532_1.png)



Oprócz powyższego projektu, do solucji dorzucę również projekt do zarządzania logiką (Class Library do apek uniwersalnych). Będzie on odpowiadał za komunikację ze stroną portalu, zarządzał powiadomieniami od strony naszej apki, a także zajmie się mapowaniem obiektów i innymi rzeczami, które w przyszłości będą dochodziły do aplikacji. Zapewne będzie trzeba stworzyć również rodzaj lokalnej bazy, do przetrzymywania historycznych powiadomień i ustawień. Nie wykluczam także powiększenie apki o kolejne moduły, które pozwolą na zarządzanie kontem, a może nawet pokuszę się o jakieś rozszerzenie funkcjonalności (jakieś dodatkowe powiadomienia?).

Trzecim projektem jest Unit Test, który będzie służył do testowania kodu. Na początek będzie to główny rdzeń solucji, tuż obok logiki. Ze względu na to, iż w pierwszej kolejności zadbać chcę o podstawowe funkcjonalności komunikacyjne pomiędzy portalem, a aplikacją - to testy jednostkowe będą głównym sposobem na sprawdzenie poprawności kodu.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-16-_53_/g_-_608x405_-_-_71411x20160315224647_0.PNG)



<blockquote>
<p>Refactoring to podstawa</p>
</blockquote>

Oczywiście taki szkielet projektu jest tylko przejściowym stadium. W miarę rozrostu aplikacji zajdzie zapewne potrzeba na podzielenie kodu na odrębne projekty, dokonanie zmian i reorganizacji. Jednakże na sam początek taki niewielki podział powinien wystarczyć.

Przejdźmy zatem do mięska...



## Logujemy się z poziomu kodu



Logowanie do aplikacji podzielić można na dwa etapy:



  * Pobranie ciasteczka


  * Zalogowanie się do portalu z użyciem ciasteczka






### Uzyskiwanie ciasteczka

 

Punkt pierwszy wymaga od nas pobrania ciasteczka z portalu. Sprawa jest prosta, musimy pozyskać ciasteczko, które będzie wykorzystane w logowaniu (po szczegóły odsyłam do [wcześniejszego wpisu](http://www.dobreprogramy.pl/djfoxer/Analiza-logowania-do-portalu-dobreprogramy.pl-uzyskujemy-dostep-do-zasobow-uzytkownika,71265.html)). W tym celu wystarczy jedynie pobrać stronę, która zwrócimy nam Id (ciasteczko), identyfikujące sesję użytkowania (jeszcze niezalogowanego) po stronie serwera.

W tym celu w z poziomu kodu należy wywołać zapytanie do serwera o dowolną stronę. Do tego zadania wytypowałem stronę z klasycznym logowaniem. Nie będziemy się przez nią w żaden sposób logować, ale pozyskamy z niej ciasteczko. Jest to najlżejsza strona i najszybciej uda się nam pobrać wymagane dane.

Kod wygląda następująco:


```csharp

            WebResponse response = null;
            WebRequest request = null;
            string cookie = string.Empty;

            //get Cookie from old login page
            request = WebRequest.Create(Const.OldLoginUrlWithTimeStamp);
            request.Method = &quot;GET&quot;;
            response = await request.GetResponseAsync();

            cookie = response.Headers
```
?.Split(&#39;;&#39;)?.FirstOrDefault();
[/code]

Do stworzenia requesta użyjemy metody Create z klasy abstrakcyjnej WebRequest.  *OldLoginUrlWithTimeStamp*  jest właściwością zwracająca adres 
```html
https://ssl.dobreprogramy.pl/Logowanie.html
```
 ze znacznikiem czasu (aby nic przypadkiem nie wpadło nam do cache). Dodajemy dodatkowo informację, że wyślemy zapytanie GETem.

Pobieranie danych zrobione jest asynchronicznie, aby nie obawiać się o zamrażanie się UI podczas połączenia.  *GetResponseAsync*  zwróci nam odpowiedź z serwera, czyli stronę z logowaniem. Nas interesuje jednak tylko ciasteczko z nagłówka, które pobierzemy prosto w ten sposób:


```csharp

            cookie = response.Headers
```
?.Split(&#39;;&#39;)?.FirstOrDefault();
[/code]

Mamy już ciasteczko. Teraz musimy zalogować się  z użyciem pobranego ciasteczka.



### Logowanie!



Przystępujemy zatem do naszego małego finału. Zakładamy, że login i hasło jest przekazywane nam w metodzie w postaci parametrów  *login*  i  *password* .

Budujemy zatem zapytanie do serwera, które zaloguje nam użytkownika.


```csharp

            request = WebRequest.Create(Const.LoginUrl);
            request.Method = &quot;POST&quot;;
            request.Headers
```
 = cookie;
            request.ContentType = &quot;application/x-www-form-urlencoded; charset=UTF-8&quot;;
            byte[] form = Encoding.UTF8.GetBytes(
                &quot;what=login&amp;login=&quot; + Uri.EscapeDataString(login)
                + &quot;&amp;password=&quot; + Uri.EscapeDataString(password) +
                &quot;&amp;persistent=true&quot;);
            using (Stream os = await request.GetRequestStreamAsync())
            {
                os.Write(form, 0, form.Length);
            }
[/code]

Podobnie jak wyżej, posłużymy się metodą  *Create*  z klasy  *WebRequest* , tym razem jednam wyślemy POSTa po adres:


```html
https://ssl.dobreprogramy.pl/Providers/LoginProvider.ashx
```


Mając już ciasteczko dodajemy go do nagłówka zapytania. Wymagane jest również ustawienie typu zawartości wysyłanych danych. Dzięki wcześniejszemu postowi wiemy, jakie dane są uzupełnianie w przeglądarce i dokładnie to same informacje przekazujemy do requesta w polu  *ContentType* .

 *&quot;Formularz&quot;*  ( *form* ) logowania budujemy również w taki sam sposób, jak podsłuchaliśmy w przeglądarce. Oprócz informacji o typie zapytania ( *what=login* ) i autologowaniu w przyszłości ( *persistent=true* ) musimy tutaj podać hasło i login użytkownika ( *login*  i  *password* ). Tutaj musimy zadbać o poprawność danych, login i hasło muszą zostać zapisane w formie, która nie spowoduje błędów w przesyłaniu danych w ten sposób. Z pomocą przyjdzie metoda  *EscapeDataString*  z wbudowanej klasy pomocniczej Uri, która  pozwoli na dodanie tzw. znaków ucieczki. Czyli np. taki tekst:


```txt
Nancy krzyknęła &quot;Hello World!&quot; do tłumu.
```


zamieni na:


```txt
Nancy krzykn\u0119\u0142a \&quot;Hello World!\&quot; do t\u0142umu.
```


Mamy zatem już przygotowany formularz, jedynie co zostało to wysłanie requestu na serwer, aby dokonać logowania. Robimy to poprzez:


```csharp
response = await request.GetResponseAsync();
```


Jeśli wszystko się udało,  *ciasteczko*  przechowywane w zmiennej  *cookie*  wskazywać będzie na sesję zalogowanego użytkownika, którego dane pobraliśmy:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-16-_53_/g_-_608x405_-_-_71411x20160316001059_0.png)



Co jeśli dane do logowanie byłyby niepoprawne? Wówczas przy wywołaniu  *GetResponseAsync*  otrzymamy wyjątek z serwera:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-16-_53_/g_-_608x405_-_-_71411x20160316001100_0.png)



Dodajmy zatem jeszcze proste (na ten czas) rozwiązanie w postaci kodu  *try..catch* , który pozwoli na detekcję błędnych danych do logowania:


```csharp
            try
            {
                response = await request.GetResponseAsync();
            }
            catch (WebException e) 
            when (((HttpWebResponse)e.Response).StatusCode == HttpStatusCode.Unauthorized)
            {
                return string.Empty;
            }
            catch (Exception)
            {
                return null;
            }
```




## Kolejne kroki?


Mamy zatem już podstawowy mechanizm do logowania. Śmiało można sprawdzać różne warianty danych przy testach jednostkowych. Zanim będziemy dalej rozbudowywali program i go zabezpieczali, w kolejnym wpisie przedstawię kod do zarządzania systemem powiadomień na portalu. 

Będzie można prześledzić sposób na pobieranie i oznaczanie powiadomień w C#, a także przedstawię mapowanie danych jak i typy informacji, jakie otrzymujemy z serwera.

Zapraszam do kolejnych odcinków z serii :)

<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>
 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-16-_53_/g_-_608x405_-_-_71411x20160315225438_0.png)

