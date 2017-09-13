---
layout:     post
title:      Zadania działające w tle w Universal Windows Platform
date:       2016-04-16 16:18:00
summary:    Aplikacja do powiadomień z portalu jest już na takim etapie, że z powodzeniem testuje ją na co dzień na swoim komputerze i smartfonie z Windows 10. Zapewne ważnym elementem jest praca w tle, nawet wówczas, gdy aplikacja nie jest uruchomiona.Dziś zaprezentuję w jaki sposób powiadomienia są pobierane ...
categories: windows programowanie urządzenia mobilne
---



Aplikacja do powiadomień z portalu jest już na takim etapie, że z powodzeniem testuje ją na co dzień na swoim komputerze i smartfonie z Windows 10. Zapewne ważnym elementem jest praca w tle, nawet wówczas, gdy aplikacja nie jest uruchomiona.


 
Dziś zaprezentuję w jaki sposób powiadomienia są pobierane w czasie, gdy aplikacja nie jest na głównym planie, a także jeśli nie została nawet otwarta. Nowa platforma od Microsoftu oferuje kilka ciekawych elementów, które pozwalają na wykonywanie zadań w tle, w odpowiedzi na zadany trigger (wyzwalacz).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416155304_0.png)





## Background Task - niezależny kod wykonywany w tle


Zadania działające w tle mogą w ciekawy sposób rozszerzyć funkcjonalność aplikacji na urządzeniu mobilnym lub desktopie. W tym celu obecnie można stworzyć kilka Background Tasków, każdy z nich może być aktywowany w zależności od potrzeb. Taki task musi implementować interfejs  *IBackgroundTask* . Działać on może nawet wówczas, gdy aplikacja nie jest uruchomiona.



### Aktywacja na zdarzenie systemowe



Można zatem stworzyć zadanie, które będzie aktywowane w odpowiedzi na zdarzenia systemowe. Mogą to być np:


  * Internet stał się dostępny/niedostępny


  * otrzymano SMS


  * użytkownik jest aktywny/nieaktywny 


  * zmienił się status sieci komórkowej


  * zmienił się stan baterii


  * zmieniła się strefa czasowa


  * dodano/usunięto aplikację z ekranu blokowania


  * inne..



Zadanie może zostać także odpalone w odpowiedzi na powiadomienia Push i zdarzenia sieci.



### Aktywacja co ustalony czas



Oczywiście można także aktywować zadania co jakiś ustalony czas, nawet gdy aplikacja nie została uruchomiona. Rozróżnia się dwa triggery:


  * MaintenanceTrigger - aktywacja co ustalony czas, gdy urządzenie podpięte jest do zasilania


  * TimeTrigger - aktywacja co ustalony czas








### Ograniczenie zdarzenia


Do zdarzeń możemy dodać warunki, jakie muszą zajść aby aktywował się kod, mogą to być np.:


  * dostępny (lub brak) Internet


  * użytkownik dostępny (lub nie)


  * inne..





## Sprawdzanie w tle powiadomień z portalu dobreprogramy.pl


Tyle teoria, jak to zatem zostało zrobione w aplikacji do odbierania zdarzeń z portalu?

W naszym przypadku posłużymy się  *TimeTrigger* , który co zadany czas sprawdzi czy są nowe powiadomienia z dobreprogramy.pl wówczas, gdy aplikacja nie jest uruchomiona. Będzie on aktywowany jeśli możliwe stanie się połączenie z Internetem.

W przypadku, gdy program będzie działał (zminimalizowany lub w tle - na desktopie lub gdy działa jako główna aplikacja - na urządzeniu mobilnym), wówczas przysłużymy się zwykłym wątkiem aktywowanym co określony czas.



### Konfiguracja



Kod, który ma działać w tle, należy dodać do projektu z typem ustawimy na  *Windows Runtime Component* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416152625_0.PNG)



Dodatkowo w pliku manifest aplikacji, należy zarejestrować zadanie w tle. W zakładce  *Declarations*   wybieramy element  *Background Tasks* :



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416153204_0.PNG)



Zaznaczamy typ taska jako  *Timer*  (+ opcja  *General* ). Ręcznie musimy podać pełny namespace do klasy, która będzie zawierała implementację  *IBackgroundTask* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416153204_1.PNG)



Pamiętajmy, że projekt głównej aplikacji musi mieć referencje do projektu z implemetacją  *IBackgroundTask* .



### Implementacja IBackgroundTask



Każda klasa, która ma działać w tle musi dziedziczyć po interfejsie  *IBackgroundTask* . Implementacja jego wymaga stworzenia metody  *Run* , która będzie uruchamiana w tle.

W naszym przypadku wygląda to następująco:

```csharp


public sealed class GetNotificationBackgroundTask : IBackgroundTask
{
        public async void Run(IBackgroundTaskInstance taskInstance)
        {
            BackgroundTaskDeferral _deferral = taskInstance.GetDeferral();
            //KOD odpowiedzialny za działanie w tle
            _deferral.Complete();
            
        }
}


```


Wywołanie metody :

```csharp


BackgroundTaskDeferral _deferral = taskInstance.GetDeferral();
_deferral.Complete();


```

powiadamia system, że zakończyliśmy zadania w przypadku, gdy działamy na wielu wątkach.



### Rejestracja zadania w tle



Zadanie rejestrujemy poprzez  *BackgroundTaskBuilder* . 


```csharp


Type thisTask = typeof(GetNotificationBackgroundTask);

var builder = new BackgroundTaskBuilder();
builder.Name = thisTask.Name;
builder.AddCondition(new SystemCondition(SystemConditionType.InternetAvailable));
var timer = new TimeTrigger(15, false);
builder.SetTrigger(timer);
builder.TaskEntryPoint = thisTask.FullName;
var task = builder.Register();


```


Dodając element, który działać będzie w tle, musimy podać nazwę taska ( *Name* ) i pełny namespace, do klasy ( *TaskEntryPoint* ), która będzie odpowiedzialna za działanie w tle. W tym przypadku pobrałem nazwę klasy i namespace z typu.

Dodałem również warunek, który sprawdzany będzie przy uruchomieniu zadania. W naszym przypadku jest to wymóg tego, aby aplikacja miała dostęp do Internetu ( *SystemConditionType.InternetAvailable* ).

Zdarzeniem, które odpowiadać będzie za uruchomienie kodu, jest zwykły timer.  *TimeTrigger*  niestety ma ograniczenie, które zostało narzucone odgórnie:

<blockquote>
<p>TimeTrigger może być uruchamiany co określony czas, ale nie może być to częściej niż 15 minut.</p>
</blockquote>

Zatem powiadomienia mogą być sprawdzane co 15 minut (jest to minimalny czas). Oczywiście mówimy tu o przypadku, gdy  *aplikacja nie jest uruchomiona* . Gdy aplikacja jest uruchomiona na desktopie/telefonie lub ewentualnie aplikacja jest zminimalizowana na desktopie, wówczas można powołać wątek, który będzie co dowolny czas sprawdzał powiadomienia. Ja zrobiłem to w taki sposób:


```csharp

 ThreadPoolTimer PeriodicTimer = ThreadPoolTimer.CreatePeriodicTimer((source) =>
{
      LoadNotification();

}, TimeSpan.FromSeconds(30));

```


<blockquote>
<p>Uruchomiona aplikacja (zminimalizowana, nieaktywna) będzie sprawdzała powiadomienia w głównym wątku co 30 sekund.</p>
</blockquote>

Jeśli przed rejestracją, chcemy sprawdzić czy zadanie zostało aktywowane, należy zrobić to w następujący sposób:


```csharp

 if (!BackgroundTaskRegistration.AllTasks.Select(x => x.Value.Name).ToList()
.Exists(x => x == GetNotificationBackgroundTask.TaskName))
 {
     GetNotificationBackgroundTask.RegisterMe();
 }

```


Można także pokusić się o sprawdzenie statusu zadań w tle. Pozwoli to na wykrycie zdarzenia, gdy np. osiągnięto limit wątków działających w tle:


```csharp

 var status = await BackgroundExecutionManager.RequestAccessAsync();

```




### Debugowanie


Ważnym elementem programowania jest debugowanie. Aby nie czekać np. 15 minut na wywołanie zadania, należy wykorzystać opcje w Visual Studio do wymuszenia odpalenia taska:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416161729_0.png)



W razie problemów, warto także przeglądać dziennik zdarzeń:

 *Dziennik aplikacji i usług -> Microsoft -> Windows -> BackgroundTaskInfrastructure -> Diagnostic*  (zaznaczając w menu  *Widok*  opcję  *Pokaż dzienniki analityczne i debugowania* ):



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416161735_0.png)





### Komunikacja aplikacja - zadania w tle


Zadania w tle są niezależnymi wątkami, które działają poza aplikacją docelową. Komunikacja z nimi odbywa się poprzez Local Storage. Jest to miejsce, gdzie każda aplikacja ma swoje własne pliki. Zarówno wątek główny aplikacji, jak i zadania w tle mogą odczytywać i zapisywać dane w tym miejscu.




## Konkurs na nazwę aplikacji trwa!


Ciągle trwa konkurs na nazwę aplikacji portalowej :) Do wygrania kody do gier na Steam! Zapraszam do dodawania swoich propozycji w komentarzach pod [wcześniejszym wpisem](http://www.dobreprogramy.pl/djfoxer/Konkurs-na-nazwe-aplikacji-dobreprogramy.pl-a-takze-niesforny-Visual-Studio,72207.html). Rozwiązanie konkursu w następnym tygodniu :)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416152607_1.jpg)





## W kolejnym odcinku...


W następnym wpisie postaram się przedstawić sposób na zapisywanie danych w Local Storage. Obecnie pierwszy kod jest już na GitHubie, ale jest jeszcze kilka rzeczy, jakie trzeba będzie dodać. Na pewno przyda się synchronizacją wątku, przy zapisie do wspólnego pliku z powiadomieniami. Może pokuszę się później o uzycie Roaming Storage, który pozwalana na dzielenie plików pomiędzy różnymi urządzeniami (wówczas można synchronizować dane pomiędzy komórką, a np. desktopem). 




<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-16-_46_/g_-_608x405_-_-_72360x20160416152607_0.png)

