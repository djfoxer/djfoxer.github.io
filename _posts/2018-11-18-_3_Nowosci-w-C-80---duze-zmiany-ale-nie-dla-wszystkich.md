---
layout:     post
title:      Nowości w C# 8.0 — duże zmiany, ale nie dla wszystkich
date:       2018-11-18 15:06:00
summary:    C# 8.0 zbliża się wielkimi krokami. Premiera planowana jest razem z .NET Core 3.0 (nieokreślona data w 2019 roku), aczkolwiek pierwsze wersje podglądowe mają być dostępne już z wersjami beta Visual Studio 2019. Co ciekawe, nowości w C# 8.0 nie będą dostępne dla wszystkich (tak, tak, klasyczny .NET Framework będzie zapewne wygaszany!).Cóż zatem nowego możemy spodziewać się w C# 8.0? Sprawdźmy to! <...
categories: programowanie
slug: Nowosci-w-C--duze-zmiany-ale-nie-dla-wszystkich,92211.html
---



C# 8.0 zbliża się wielkimi krokami. Premiera planowana jest razem z .NET Core 3.0 (nieokreślona data w 2019 roku), aczkolwiek pierwsze wersje podglądowe mają być dostępne już z wersjami beta Visual Studio 2019. Co ciekawe, nowości w C# 8.0 nie będą dostępne dla wszystkich (tak, tak, klasyczny .NET Framework będzie zapewne wygaszany!).

Cóż zatem nowego możemy spodziewać się w C# 8.0? Sprawdźmy to! 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2018-11-18-_3_/g_-_-x-_-_-_x6dea61f5-a68a-4528-a982-5ea5603b88c8.png)





### Nullowalne typy referencyjne


Ktoś w Microsofcie stwierdził, że stanowczo za dużo w życiu programistów jest wyjątków  *NullReferenceExceptions* . Od C# 8.0 wprowadzone zostaną nullowalne typy referencyjne. Pozwolić to ma na lepsze zarządzanie nullami w kodzie i uniknięcie wyjątków w najmniej oczekiwanych momentach. 

Prześledźmy to na przykładzie popularnego  *stringa. * Zadeklarowana do tej pory zmienna:




```csharp
string s = null; //Warning: null w referencyjnym typie nienullowalnyn
```


będzie zgłaszać ostrzeżenie (nie błąd!) o tym, że null podstawiany jest do nienullowalnego typy referencyjnego. W celu uniknięcia ostrzeżenia należy zadeklarować nowy, nullowalny typ referencyjny. 




```csharp
string? s = null; //a, teraz ok
```


Dodatkowo kompilator będzie analizował kod, aby sprawdzić czy przypadkiem nie natrafimy na nulla używając nullowalnego typu referencyjnego. Jeśli tak się stanie - zostanie pokazane ostrzeżenie. Można będzie tego uniknąć używając sprawdzenia czy dana zmienna nie jest nullem. Krótki przykład przedstawiający jak to będzie działać w C# 8.0:




```csharp
void M(string? ns)            // ns is nullable
{
    WriteLine(ns.Length);     // WARNING: may be null
    if (ns != null) 
    { 
        WriteLine(ns.Length); // ok, not null here 
    } 
    if (ns == null) 
    { 
        return;               // not null after this
    }                         
    WriteLine(ns.Length);     // ok, not null here
    ns = null;                // null again!
    WriteLine(ns.Length);     // WARNING: may be null
}
```


W zapowiedzi nie ma nic już o operatorze  *"!"* , który miał mówić kompilatorowi, o tym że programista jest świadom tego co robi, dzięki czemu ostrzeżenie miało nie być pokazywane:




```csharp
void M(Person p)
{
    WriteLine(p.MiddleName.Length);  // WARNING: may be null
    WriteLine(p.MiddleName!.Length); // ok, you know best!
}
```


[b] *Wg mnie..:* [/b] Nullowalne typy referencyjne to ciekawy krok do przodu w świecie programowania obiektowego w C#. Niepokoić może trochę to, że przejście na C# 8.0 w istniejącym już projekcie będzie powodować olbrzymią ilość warningów przy kompilacji. Z drugiej strony może to pomóc w utrzymaniu kodu wolnego od typowego wyjątku, jakim jest  *NullReferenceExceptions* . Zobaczymy jak to finalnie wyjdzie. Na pewno nie obędzie się bez refactoringu istniejącego już kodu, po przeskoczeniu na C# 8.0. Co nie zmienia tego, że jestem na tak :) 


### Domyślna implementacja w interfejsie


Drugą ciekawą nowością są domyślne implementacje w tworzonym interfejsie. Od C# 8.0 można będzie dodać domyślną implementację w interfejsie i użyć jej w klasie, która dziedziczy po tym interfejsie. Przykładowy kod z blogu MSDN w C# 8.0:




```csharp
interface ILogger
{
    void Log(LogLevel level, string message);
    void Log(Exception ex) => Log(LogLevel.Error, ex.ToString()); // New overload
}

class ConsoleLogger : ILogger
{
    public void Log(LogLevel level, string message) { ... }
    // Log(Exception) gets default implementation
}
```


W przykładzie ConsoleLogger brak implementacji Log(Exception ex), nie spowoduje błędu kompilacji, gdyż zostanie wzięta domyślna implementacja z interfejsu ILogger. 

[b] *Wg mnie... * [/b]Krok ciekawy, coś podobnego zostało zaprezentowane już w Javie 8. Nie jest to nic szczególnego wg mnie, gdyż do tej pory w większości przypadków domyślny kod znajdował się np. w dziedziczonej klasie abstrakcyjnej. Ciekawe, ale nie jest to jakiś killer-ficzer, czy coś na co wiele osób czekało. Bez szału.


### Nowe typy: Index i Range


C# 8.0 wprowadza także dwa typy: Index i Range.

Index służy do indeksowania. Możemy szybko dostać się do elementu pod konkretnym indeksem. Co ciekawe indeksować można od początku lub od końca, w tym ostatnim przypadku użyjemy operatora ^:




```csharp
Index i1 = 3;  // indeks 3  - liczony od początku
Index i2 = ^4; // indeks 4 - liczony od końca
int[] a = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
Console.WriteLine($"{a[i1]}, {a[i2]}"); // "3, 6"
```


Typ Range jest połączeniem dwóch typów Index i pozwala na wycięcie elementów z zadanego zakresu:




```csharp
var slice = a[i1..i2]; // { 3, 4, 5 }
```


[b] *Wg mnie...* [/b] Mała rzecz, ale może być całkiem przydatna szczególnie ten indeks liczony od końca. Mały, ale zdecydowany plusik.


### Async streams


Nowa wersja C# wprowadza także asynchroniczną odmianę  *IEnumerable<T>* , czyli  *IAsyncEnumerable<T>* . W tym momencie będzie to zapewne duże ułatwienie w konsumpcji/tworzeniu strumieni danych wytwarzanych przez IoT czy chmurę. Będzie zatem można tego użyć w następujący sposób:




```csharp
async IAsyncEnumerable<int> GetBigResultsAsync()
{
    await foreach (var result in GetResultsAsync())
    {
        if (result > 20) yield return result; 
    }
}
```


[b] *Wg mnie...* [/b] Cóż, ok. Zapewne znajdą się osoby, do których ten ficzer jest bezpośrednio targetowany. 


### Pattern matching z rekurencją


Wprowadzony [pattern matching w C# 7 ](http://blog.djfoxer.pl/Nowosci-w-C-7-jest-kontrowersyjnie,76985.html)będzie mógł zawierać inny pattern matching. Od C# 8.0 będzie można używać zagnieżdżonego pattern matching:




```csharp
IEnumerable<string> GetEnrollees()
{
    foreach (var p in People)
    {
        if (p is Student { Graduated: false, Name: string name }) yield return name;
    }
}
```


W powyższym przykładzie z MSDN szukamy obiektu  *Poeple* , który jest typu  *Student* , ma dodatkowo właściwość  *Graduated*  ustawioną na  *false, a*  właściwość name nie jest nullem.

[b]Wg mnie... [/b]Całkiem ciekawe rozwinięcie pattern matchingu. Coraz częściej używam PM w pracy i całkiem nieźle pomaga w zachowaniu przejrzystego kodu. Oczywiście nadużycie może doprowadzić do tego, iż kod będzie delikatnie trudny do czytania, ale tu już trzeba będzie zdać się na umiar.


### Wyrażenia switch


Kolejny element rozszerzający pattern matching: wyrażenia switch. W C# 8.0 będzie można użyć switcha, który zredukuje trochę kodu i przyspieszy tworzenie prostszych switchy:




```csharp
var area = figure switch 
{
    Line _      => 0,
    Rectangle r => r.Width * r.Height,
    Circle c    => Math.PI * c.Radius * c.Radius,
    _           => throw new UnknownFigureException(figure)
};
```


 [b]Wg mnie...[/b] Nowe elementy do pattern matchingu zawsze na propsie!


### Docelowy typ w wyrażeniach new


Na koniec mały element, który nadchodzi wraz z C# 8.0. Tworząc nowe elementy np. w tablicy, typ wykrywany będzie na podstawie kontekstu, co pozwoli na ominięcie nazwy typu w deklaracji:




```csharp
Point[] ps = { new (1, 4), new (3,-2), new (9, 5) }; // all Points
```


[b]Wg mnie...[/b] Niech i tak będzie, ok :)


### Nie dla psa kiełbasa!


Omawiane ficzery będą częścią .NET Standard 2.1, czyli na pewno spotkamy je w .NET Core 3.0 czy Xamarinie, ale... nie wszystkie trafią do .NET Framework 4.8! W ten sposób domyślna implementacja w interfejsie nie trafi do .NET Frameworku! Czy to już ten moment, kiedy Microsoft zacznie wygaszanie klasycznego .NET Frameworku na rzecz nowego .NET Core? Zobaczymy, ale warto mieć to na uwadze, że niedługo może trzeba będzie zacząć przesiadkę ze starego .NET, na .NET Cora....

Warto pamiętać, że do finalnego C# 8.0 mogą trafić jeszcze jakiś ficzery, albo część może wylecieć, wszak do premiery mamy jeszcze trochę czasu.

Na podstawie: [Building C# 8.0](https://blogs.msdn.microsoft.com/dotnet/2018/11/12/building-c-8-0/). 
Wcześniejsze wpisy: [Nowości w C# 7.0](http://blog.djfoxer.pl/Nowosci-w-C-7-jest-kontrowersyjnie,76985.html), [Nowości w C# 6.0](http://blog.djfoxer.pl/Nowosci-w-C-6-coz-ciekawego-otrzymujemy,74772.html). 





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2018-11-18-_3_/g_-_-x-_-_-_x7bc13a4e-65c4-42d8-8cba-59d772428eaf.png)
