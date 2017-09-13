---layout:     post
title:      Pierwsza wersja aplikacji, ciasteczka i refactoring  — dobreprogramy na Windows 10
date:       2016-03-27 15:42:00
summary:    Wcześniejsze dwa wpisy przedstawiały kompletny sposób na zalogowanie się do portalu i zarządzanie powiadomieniami. W momencie tworzenia już UI, pod Universal Windows Platform (UWP), okazało się jednak, że potrzebny jest mały refactoring, wymuszony przez cachowanie ciasteczek, które powoduje w pewnyc...
categories: windows programowanie urządzenia mobilne
---



Wcześniejsze dwa wpisy przedstawiały kompletny sposób na [zalogowanie się do portalu](http://www.dobreprogramy.pl/djfoxer/Logujemy-sie-do-dobreprogramy.pl-z-poziomu-kodu-C-wprowadzenie-do-projektu,71411.html) i [zarządzanie powiadomieniami](http://www.dobreprogramy.pl/djfoxer/Powiadomienia-z-dobreprogramy.pl-w-C-z-dziennika-dewelopera,71524.html). W momencie tworzenia już UI, pod Universal Windows Platform (UWP), okazało się jednak, że potrzebny jest  *mały*  refactoring, wymuszony przez cachowanie ciasteczek, które powoduje w pewnych przypadkach problemy. Dodatkowo zmieniło się założenie co do przechowywania danych użytkownika w apce, a także powstały dwa pierwsze ekrany do próbnej wersji aplikacji.



## Cachowanie ciasteczek



Plan na napisanie aplikacji zakładał to, iż przy pierwszym requeście będziemy pobierali ciasteczko, a następnie do logowania i pozostałych działań na powiadomieniach będzie ono przesyłane z każdy zapytaniem. Był to dobry pomysł, ale niestety okazało się, że nadpisanie ciasteczka per request nie jest idealne.

Otóż ciasteczko z ID sesji przy logowaniu jest cachowane  *odgórnie*  i przesyłane w kolejnych zapytaniach. Problemem jest wówczas to, iż dodając do zapytania własne ciasteczko z ID sesji, idzie ono razem z poprzednią sesją (dorzucaną automatycznie). Wówczas np. po błędnym zalogowaniu (lub  *wylogowaniu* ), nadal mogliśmy pobierać powiadomienia z poprzednio zalogowanego użytkownika. 

Rozwiązaniem było zatem czyszczenie globalnego ciasteczka i zapisywanego w kontekście aplikacji. Stwierdziłem jednak, że można to rozszerzyć, wykorzystując powyższy fakt i przy okazji zrobić mały refactoring.




## Refactoring





### HttpClient

 

Na początek pozbyłem się klasy WebRequest i użyłem  [HttpClient](https://blogs.windows.com/buildingapps/2015/11/23/demystifying-httpclient-apis-in-the-universal-windows-platform/) (z Windows.Web.Http, nie z System.Net.Http), co było sugerowane w komentarzach. Faktycznie WebRequest w UWP był wrzucony tylko z  *czystej przyzwoitości*  i raczej nie powinno się już go używać w tego typu apkach. Główną jednak zaletą jest czystsza implementacja, niż w przypadku WebRequesta.



### Brak jawnego pobierania ciasteczka



Wyrzuciłem kod, który tworzył pierwsze zapytanie do strony. Jego jedynym celem było pobrania ciasteczka, które miało być jawnie przechowywane i wysyłane przy każdym następnym requeście. Nie jest to zupełnie już potrzebne. Wystarczy, że usuniemy ciasteczka związane z sesją, wówczas przy poprawnym logowaniu serwer zwróci nam żądane ciasteczko. W ten sposób zaoszczędziliśmy zarówno na szybkości, jak i na ilości przesyłanych danych. Obecnie przed logowaniem czyszczone są ciasteczka: typowe .NETowe  *ASP.NET_SessionId* , a także dodatkowe -  *NGDP_Auth* .



### Bez jawnej obsługi cookie



Ostatni element to samo ciasteczko z sesją. Obecnie nie ma potrzeby zarówno przechowywania go jawnie w aplikacji, jak i  *doklejania*  do każdego zapytania. Cache w aplikacji sama będzie trzymał ciasteczko, niezbędne do identyfikacji użytkownika. Wbudowany cache na poziomie systemu (per aplikacja), działa nawet po zamknięciu programu, więc odpada tutaj potrzeba przechowywania go jawnie.


Teraz przy uruchamianiu aplikacji, a przed logowaniem, wystarczy sprawdzić, czy istnieje jeszcze  *nieprzeterminowane*  ciasteczko z ID sesji w aplikacji.
Dodatkowo, pozwoli to na stworzenie aplikacji, w której nie będzie przetrzymywanego hasła, a także jawnego trzymania ciasteczka do sesji zalogowanego użytkownika. Nie trzeba się martwić zatem o swoje dane :)


Obecnie logowanie wygląda w następujący sposób:


```csharp

            using (var httpClient = new HttpClient())
            {
                request = new HttpRequestMessage(HttpMethod.Post, new Uri(Const.UrlLogin));
                request.Content = new HttpFormUrlEncodedContent(new
```
 {
                    new KeyValuePair&lt;string, string&gt;(&quot;what&quot;, &quot;login&quot;),
                    new KeyValuePair&lt;string, string&gt;(&quot;login&quot;, login),
                    new KeyValuePair&lt;string, string&gt;(&quot;password&quot;, password),
                    new KeyValuePair&lt;string, string&gt;(&quot;persistent&quot;, &quot;true&quot;),
                });

                try
                {
                    response = await httpClient.SendRequestAsync(request);
                }
                catch (Exception)
                {
                    return false;
                }
            }

            return response.StatusCode == Windows.Web.Http.HttpStatusCode.Ok;
[/code]

Samo pobieranie powiadomień to niemalże dwie linijki kodu:


```csharp

            using (var httpClient = new HttpClient())
            {
                request = new HttpRequestMessage(
                                HttpMethod.Get, new Uri(Const.UrlNotifyWithTimeStamp));
                response = await httpClient.SendRequestAsync(request);
            }

```


Czyszczenie ciasteczek robione jest w następujący sposób:


```csharp

            var httpFilter = new Windows.Web.Http.Filters.HttpBaseProtocolFilter();

            httpFilter.CookieManager.DeleteCookie(
                new HttpCookie(Const.CookieSessionName, Const.UrlDomain, &quot;/&quot;));

            httpFilter.CookieManager.DeleteCookie(
                new HttpCookie(Const.NGDP_Auth, Const.UrlDomain, &quot;/&quot;));

```




## Aplikacja - pierwsza wersja




Oczywiście, jak już wszystko zaczęło działać postanowiłem zrobić wstępny projekt, który będzie pozwalał na przetestowanie  *naocznie*  nowych elementów.

Do tworzenia aplikacji używam[ MVVM Light Toolkit](https://mvvmlight.codeplex.com/). Co ciekawe, dostępne są już nowe XAML Behaviors, które stworzenie zostały m.in.  pod UWP (domyślny szablon z MVVM Lighta używa starej wersji, dedykowanej Windows 8.1). Zapewne niedługo dorzucę także [Cimbalino Toolkit](https://cimbalino.org/), który znacznie uprzyjemnia pracę z UWP . 

Obecne efekty nie są  *piękne* , ale pozwalają na doszlifowywanie obecnych rozwiązań i tworzenie nowych elementów. Poniżej wrzucam kilka screenów z aplikacji na Windows 10 i Windows 10 Mobile. Zaznaczam, że nie są to mockupy, a screeny z działającej już aplikacji ;)



### Windows 10





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327150838_0.png



)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327150839_0.png





### Windows 10 Mobile




)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327151936_0.PNG



)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327151936_1.PNG






## W kolejnym odcinku...



W przyszłych commitach zapewne postaram się doszlifować listę z powiadomieniami. Jednakże to nie ona jest priorytetem. Chciałbym w następnym wpisie przedstawić sposób na działanie aplikacji w tle. Całość będzie sprowadzała się do pobierania co jakiś czas listy z powiadomieniami. Jeśli okaże się, że jest jakieś nowe powiadomienie, wówczas system wyświetli odpowiedni komunikat:

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327152200_0.PNG



)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327152206_0.png



Zatem, do następnego ;)

<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>
)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-27-_50_/g_-_608x405_-_-_71727x20160327154001_0.png

)