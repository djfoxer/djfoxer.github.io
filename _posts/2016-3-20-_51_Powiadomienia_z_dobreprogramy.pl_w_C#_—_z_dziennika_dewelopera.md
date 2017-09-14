---
layout:     post
title:      Powiadomienia z dobreprogramy.pl w C# — z dziennika dewelopera
date:       2016-03-20 10:56:00
summary:    Prace ku stworzeniu uniwersalnej aplikacji Windows 10 (+ Mobile) obsługującej powiadomienia z portalu dobreprogramy.pl posuwają się na przódu. We wcześniejszym poście przedstawiłem kod (plus projekt w VS), który służy do logowania się na swoje konto z poziomu C#. Został nam zatem ostatni etap w przygotowaniu serca naszej aplikacji - zarządzanie powiadomieniami. Zatem do dzieła!Pobieramy powiadomie...
categories: windows programowanie urządzenia mobilne
---



Prace ku stworzeniu uniwersalnej aplikacji Windows 10 (+ Mobile) obsługującej powiadomienia z portalu dobreprogramy.pl posuwają się na przódu. We [wcześniejszym poście](http://www.dobreprogramy.pl/djfoxer/Logujemy-sie-do-dobreprogramy.pl-z-poziomu-kodu-C-wprowadzenie-do-projektu,71411.html) przedstawiłem kod (plus projekt w VS), który służy do logowania się na swoje konto z poziomu C#. Został nam zatem ostatni etap w przygotowaniu  *serca*  naszej aplikacji - zarządzanie powiadomieniami. Zatem do dzieła!



## Pobieramy powiadomienia z portalu w formacie JSON


Analiza sposobu działania powiadomień na portalu została przedstawiona w poście: [Analizujemy kod portalu dobreprogramy.pl — czyli jak działa system powiadomień](http://www.dobreprogramy.pl/djfoxer/Analizujemy-kod-portalu-dobreprogramy.pl-czyli-jak-dziala-system-powiadomien,71145.html). Dziś przejdziemy już jednak do kodowania.

Zacznijmy zatem od pobrania JSONa z listą powiadomień dla zalogowanego użytkownika. Zakładamy oczywiście, że posiadamy już ciasteczko (w kodzie jest to zmienna  *cookie* ), które identyfikuje zalogowanego użytkownika. Opis w jaki sposób jest to zrobione znajduje się w ostatnim wpisie ([Logujemy się do dobreprogramy.pl z poziomu kodu C#](http://www.dobreprogramy.pl/djfoxer/Logujemy-sie-do-dobreprogramy.pl-z-poziomu-kodu-C-wprowadzenie-do-projektu,71411.html)).


```csharp

            request = WebRequest.Create(Const.NotifyUrlWithTimeStamp);
            request.Headers["Cookie"] = cookie;

            response = await request.GetResponseAsync();

            string pageSource;
            using (StreamReader sr = new StreamReader(response.GetResponseStream()))
            {
                pageSource = sr.ReadToEnd();
            }

```


Podobnie jak przy logowaniu, tworzymy zapytanie do serwera poprzez użycie metody z klasy abstrakcyjnej WebRequest. Naszym adresem docelowym jest:


```html
http://www.dobreprogramy.pl/Providers/NotifyHelper.ashx?ping=ping&_=znacznik_czasu
```


Oczywiście zmienna  *znacznik_czasu*  będzie generowana przez nasz kod przy każdym zapytaniu. Jest to nic innego jak aktualna data JavaScript jako int (ilość milisekund od 1 stycznia 1970 roku).

Ważnym elementem jest tutaj uzupełnienie nagłówka o ciasteczko, jakie pozyskaliśmy na etapie logowania. W kolejnych krokach pobieramy zapytanie z serwera, czyli string posiadający odpowiedź w JSONie:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-20-_51_/g_-_608x405_-_-_71524x20160318181817_0.png)



## Praca z JSONem - Json.NET na ratunek!


Zostaje nam zatem  przerobienie JSONa na coś bardziej  *zjadliwego* . Celem jest stworzenie obiektów nowej klasy, które będą reprezentować powiadomienia z portalu. Chcąc ułatwić pracę z JSONem, nie trzeba tworzyć klas pośrednich lub ręcznie parsować stringa. Posłużymy się tutaj deserializatorem z frameworku [Json.NET](http://www.newtonsoft.com/json). W tym celu do projektu dodajemy przez NuGeta pakiet  *Newtonsoft.Json* . Nasz kod uzupełniamy o linijkę:


```csharp

            var respList = (JObject)JsonConvert.DeserializeObject(pageSource);

```


Pozwoli to nam na operowanie na danych w znacznie wygodniejszy sposób:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-20-_51_/g_-_608x405_-_-_71524x20160318183229_0.png)



## Jak wygląda powiadomienie?


W celu przechowywania powiadomień w aplikacji (bazka SQLite, a może coś bardziej trywialnego, jak plik XML ładowany, tylko częściowo, na wejście do aplikacji - to jeszcze kwestia otwarta). W tym celu stworzyłem klasę, która będzie przetrzymywała dane:


```csharp


    public class Notification
    {
        public string Id { get; set; }

        public string PublicationId { get; set; }

        public string Avatar { get; set; }

        public string CustomText { get; set; }

        public string Title { get; set; }

        public string TargetUrl { get; set; }

        public DateTime AddedDate { get; set; }

        public NotificationType TypeValue { get; set; }

        public NotificationStatus Status { get; set; }

        public string UserName { get; set; }
    }


```


Pola są odwzorowaniem danych z JSONa, dodatkowo uzupełnione o bardziej  *strawne*  formaty odnośnie statusu powiadomienia (enum NotificationStatus), typu powiadomienia (enum NotificationType), a także daty przekonwertowanej na format DateTime.

Statusy powiadomień mamy dwa (w tym jeden własny, gdyby coś nowego się pojawiło:   *Unknown* ). Typów notyfikacji jest znacznie więcej. Całość przedstawia się następująco:


```csharp


        public enum NotificationType
        {
            Unknown = -1,
            Comment = 0,
            CommentBlog = 1,
            ProgramUpdate = 2,
            Contest = 3,
            FriendsAccept = 4,
            FriendsInvite = 5,
            BlogAnnotation = 6,
            PrivateMsg = 7,
            Mention = 8,
            License = 9,
            Badges = 10,
        }

        public enum NotificationStatus
        {
            Unknown = -1,
            New = 0,
            Old = 1
        }


```


Typy powiadomień w JSONie są w formie tekstu, więc parsujemy je wg następującego schematu:


```csharp


        public static NotificationType ParseToNotificationType(string typeString)
        {
            if (string.IsNullOrWhiteSpace(typeString))
            {
                return NotificationType.Unknown;
            }

            typeString = typeString.ToLower();
            switch (typeString)
            {
                case "comment":
                    return NotificationType.Comment;
                case "comment_blog":
                    return NotificationType.CommentBlog;
                case "program_update":
                    return NotificationType.ProgramUpdate;
                case "contest":
                    return NotificationType.Contest;
                case "friends_accept":
                    return NotificationType.FriendsAccept;
                case "friends_invite":
                    return NotificationType.FriendsInvite;
                case "blog_annotation":
                    return NotificationType.BlogAnnotation;
                case "private_msg":
                    return NotificationType.PrivateMsg;
                case "mention":
                    return NotificationType.Mention;
                case "license":
                    return NotificationType.License;
                case "badges":
                    return NotificationType.Badges;
                default:
                    return NotificationType.Unknown;
            }
        }


```




## JSON => Notification

Samo parsowanie z JSONa na nasz obiekt Notification jest trywialnie proste dzięki Json.NET:


```csharp


            if (respList.HasValues)
            {
                var c = respList.First.First;

                for (int i = 0; i < c.Count(); i++)
                {
                    var ele = (JProperty)c.ElementAt(i);
                    Notification n = JsonConvert.DeserializeObject<Notification>(ele.Value.ToString());

                    n.AddedDate = new DateTime(1970, 1, 1).AddMilliseconds((long)(((JValue)ele.Value["Data"]).Value));
                    n.TypeValue = Enum.ParseToNotificationType(((JValue)ele.Value["Type"]).Value.ToString());
                    n.PublicationId = ele.Name.Split(':')[0];
                    n.Id = ele.Name.Split(':')[1];
                    notList.Add(n);
                }
            }


```


Głównym rdzeniem jest tutaj:


```csharp
Notification n = JsonConvert.DeserializeObject<Notification>(ele.Value.ToString());

```


Nie chciałem się już bawić w jakieś convertery, więc ręcznie zamieniłem pola, które nie mogą być automatycznie zmapowane: AddedDate (rzutowanie daty z JS na DateTime), TypeValue (rzutowanie na enuma) oraz Id i PublicationId (trzeba rozdzielić oryginalne pole Name).

W taki oto sposób otrzymujemy piękną listę powiadomień w C#:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-20-_51_/g_-_608x405_-_-_71524x20160318184134_0.png)


Na takiej liście można już spokojnie pracować 


## Powiadomienie - odczytywanie/usuwanie
 

Zostało jeszcze dodanie metody, które oznaczy powiadomienie jako odczytane i usunięte. Wystarczy tutaj dodać mały kawałek kodu:


```csharp


            var request = WebRequest.Create(Const.NotifyUrlRaw);
            request.Headers["Cookie"] = cookie;
            request.ContentType = "application/x-www-form-urlencoded; charset=UTF-8";
            request.Method = "POST";

            byte[] form = Encoding.UTF8.GetBytes(string.Format("{1}%5B%5D={0}", id, method));
            using (Stream os = await request.GetRequestStreamAsync())
            {
                os.Write(form, 0, form.Length);
            }
            var resesponse = await request.GetResponseAsync();


```


Wysyłamy zapytanie pod adres: (pamiętając o ciasteczku)


```html
http://www.dobreprogramy.pl/Providers/NotifyHelper.ashx
```


. Tym razem jednak dodajemy prostego forma, który zawiera  *id*  powiadomienia i typ akcji ( *method = markAsRead/deleteNotify* ) do wykonania na powiadomieniu (odczytanie/usunięcie). Oczywiście request uzupełniony jest o typ zawartości i metodę wysyłania zapytania.

W ten sposób  stworzyliśmy pełnoprawny mechanizm do zarządzania powiadomieniami z portalu dobreprogramy.pl z poziomu kodu w C#.



## Kolejne kroki?

Główny mechanizm do logowania i zarządzania powiadomieniami już mamy. Myślę, że w następnym tygodniu uda mi się  *złożyć*  coś, co nie będzie wyglądać dobrze :P , ale będzie działać w tle i pokazywać powiadomienia w Windows 10. Zobaczymy, czy uda się ten plan osiągnąć przed Wielkanocą i/lub maratonem  w Dębnie ;) 

Zapraszam do kolejnych odcinków z serii :)


> Aktualne źródła można znaleźć na GitHub pod adresem:
> [https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-20-_51_/g_-_608x405_-_-_71524x20160319134909_0.png)
