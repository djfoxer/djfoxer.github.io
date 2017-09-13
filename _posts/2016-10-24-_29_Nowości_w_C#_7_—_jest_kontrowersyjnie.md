---layout:     post
title:      Nowości w C# 7 — jest kontrowersyjnie
date:       2016-10-24 21:42:00
summary:    Jakiś czas temu pisałem o nowościach jakie wprowadza finalna wersja C# 6. Wówczas zmiany można było przetestować w Visual Studio 2015 i spokojnie zacząć ich używać na co dzień na środowisku produkcyjnym.Będąc na tegorocznym .NET DeveloperDays słynny Jon Skeet delikatnie musnął nowości w C# 7, pokazu...
categories: porady programowanie
---



Jakiś czas temu pisałem o nowościach jakie wprowadza [finalna wersja C# 6](http://www.dobreprogramy.pl/djfoxer/Nowosci-w-C-6-coz-ciekawego-otrzymujemy,74772.html). Wówczas zmiany można było przetestować w Visual Studio 2015 i spokojnie zacząć ich używać na co dzień na środowisku produkcyjnym.

Będąc na tegorocznym .NET DeveloperDays słynny Jon Skeet delikatnie musnął nowości w C# 7, pokazując Tuple i dekompozycję. Pomimo tego opinie o zmianach były dość podzielone (z przewagą tych negatywnych).

Sprawdźmy zatem całościowo jakie nowości szykują się w C# 7. Obecnie (gdy piszę te słowa) dostępne jest już testowe wydanie Visual Studio 15 (Preview 5), a także wraz z nim podglądowa wersja C# 7.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-10-24-_29_/g_-_608x405_-_-_76985x20161024211944_0.png







## Wymagania


W celu przetestowania C# 7 potrzebujemy:


  * [Visual Studio 15](https://www.visualstudio.com/en-us/news/releasenotes/vs15-relnotes) - obecnie w wersji Preview 5


  * Dodanie do projektu paczki System.ValueTuple z NuGeta, jeśli chcemy &quot;pobawić się&quot; nowymi Tuplami
)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-10-24-_29_/g_-_608x405_-_-_76985x20161024210935_0.PNG









## Pattern matching


Jednym z ciekawszych  *ficzerów*  w nowej odsłonie C# jest Pattern matching. Funkcjonalność ta daje name możliwość sprawdzenia warunku wartości, a następnie przetworzenie tej wartości, jeśli warunek jest prawdziwy. Patterns są nowymi elementami języka C#. W obecnej fazie do dyspozycji mamy następujące wzorce:



  * constant patterns:  *c*  - gdzie  *c*  jest wyrażeniem constant w C#, wzorzec testuje czy wejście jest równe wyrażeniu  *c* 


  * type patterns:  *T x*  - gdzie  *T*  jest typem, a  *x*  identyfikatorem, wzorzec sprawdza czy wejście jest typu  *T*  i jeśli tak jest wartość z wejścia podstawia pod nową zmienną  *x*  typu  *T* 


  * var patterns: *var x*  - gdzie  *x*  jest nazwą nowej zmiennej, wzorzec (sprawdzenie jest zawsze prawdziwe) jedynie ustawia wartość z wejścia pod nową zmienną  *x*  o typie takim jak wejście



W tym momencie C# 7 rozszerza dwie konstrukcje języka o pattern matching:  *is*  a także  *case* .

W przypadku  *is*  otrzymujemy możliwość umieszczenia wzorca po prawej stronie, zamiast typu, np.:


```csharp

public void CheckPackageCode(object code)
{
    if (code is null) return;
    if (!(code is string packageCode)) return;
    if (packageCode is &quot;errorCode&quot;) return;
    Console.WriteLine($&quot;correct code: {packageCode}&quot;);
}

```


Konstrukcja w  *case*  pozwala na więcej, a także przejrzystość kodu jest wówczas znacznie większa. 


```csharp

public void CheckData(Vehicle vehicle)
{
    switch (vehicle)
    {
        case Tank t:
            t.Shot();
            break;
        case Car c when c.DoorCount == 4:
            Console.WriteLine($&quot;sedan with {c.DoorCount} doors&quot;);
            break;
        case Motorbike b when b.IsHelmetAttached:
            Console.WriteLine($&quot;motorbike ready to go!&quot;);
            break;
        case null:
            Console.WriteLine(&quot;no vehicle!&quot;);
            break;
        default:
            break;
    }
}

```




### Opinia


Ciekawa funkcjonalność, która nie od początku przypadnie do gustu wszystkim, ale zapewne z biegiem czasu zyska zwolenników. Ciekawi mnie, o jakie dodatkowe konstrukcje rozszerzy Microsoft zastosowanie pattern matching w finalnej wersji C# 7.



## Tuples


Klasę Tuple wprowadzono w C# 4. Miała być ona alternatywą do tworzenia &quot;prywatnych&quot; dedykowanych klas w przypadku, gdy np. chcemy jednorazowo zwrócić kilka wartości z metody.

Wraz z C# 7 otrzymujemy typy tuple i literały tuple.


```csharp

public (string, string, int) GetUserData(int id)
{
    //load data from db
    return (&quot;Zygmunt&quot;, &quot;zygi&quot;, 123009);
}

```


W ten sposób możemy zwrócić dane znacznie szybciej niż poprzez użycie klasy Tuple. Zwracane dane będą miały publiczne pola Item1, Item2, (...) podobnie jak miało to miejsce wcześniej:


```csharp

var data = GetUserData(5);
Console.WriteLine($&quot;data : {data.Item1},{data.Item2},{data.Item3}&quot;);

```


Jednakże teraz nic nie stoi na przeszkodzie, aby ponazywać poszczególne pola:


```csharp

public (string name, string login, int phone) GetUserData(int id)
{
    //load data from db
    return (&quot;Zygmunt&quot;, &quot;zygi&quot;, 123009);
}

```


lub jeszcze w inny sposób:


```csharp

public (string, string, int) GetUserData(int id)
{
    //load data from db
    return (name: &quot;Zygmunt&quot;, login: &quot;zygi&quot;, phone: 123009);
}

```


wówczas w kodzie do poszczególnych pól odwołamy się poprzez nadane nazwy:


```csharp

var data = GetUserData(5);
Console.WriteLine($&quot;data : {data.name},{data.login},{data.phone}&quot;);

```




### Opinia


Przez wielu klasy Tuple do dziś są na cenzurowanym i nie bez przyczyny. Łatwo o zaciemnienie kodu właściwościowymi Item1, Item2,... . Kolejne wcielenie tupli nie przysporzy raczej olbrzymiej liczby zwolenników temu rozwiązaniu. Kod delikatnie zyska na czytelności poprzez aliasy, ale nadal obiekty będą posiadały prócz własnych nazw... pola Item1, Item2... Oprócz tego, że w oczy nie będzie kuła nazwa Tuple (wywołująca u niektórych słuszną alergię), nie zyskamy aż tak wiele. Faktem jednak jest, że aliasy pomogą w znacznie przyjemniejszej pracy z tuplami.



## Deconstruction


Z Tuplami związana jest również nowa funkcjonalność - dekonstrukcja. Dzięki niej możemy obiekty Tuple (ale również i zwykłe klasy) rozdzielić na dedykowane zmienne. Przykład z punktu wyżej możemy rozbić zatem na różne sposoby:


```csharp

(string name, string login, int phone)  = GetUserData(5);

```



```csharp

(var name, var login, var phone)  = GetUserData(5);

```




```csharp

var (name,  login, phone)  = GetUserData(5);

```


a nawet przypisać do istniejących zmiennych:


```csharp

(name,  login, phone)  = GetUserData(5);

```


Dekonstrukcję można wykonać na tuplach, ale również na obiektach własnych klas. W tym celu należy do deklaracji klasy dodać metodę:


```csharp

public void Deconstruct(out T1 x1, ..., out Tn xn) { ... }

```


Np.:


```csharp

public class User
{
    public string Name { get; set; }
    public string Login { get; set; }
    public int Phone { get; set; }
    public string Address { get; set; }

    public User(string name, string login, int phone)
    {
        Name = name;
        Login = login;
        Phone = phone;
    }

    public void Deconstruct(out string name, out string login, out int phone)
    {
        name = Name;
        login = Login;
        phone = Phone;
    }
}

```


Wówczas mając obiekt


```csharp

User u = new User(&quot;Zenek&quot;, &quot;mis&quot;, 0800);

```


Możemy dokonać jego dekonstrukcji w trywialny sposób:


```csharp

var (userName, userLogin, userPhone) = u;

```


Sugeruje się, że dekonstrukcja we własnych klasach będzie zapewne używana jako &quot;odwrotność&quot; konstruktora. Czas pokaże. Warto zauważyć, że dekonstruktor przyjmuję parametry wyjściowe i nie zwraca typu. Dzięki temu można przeciążyć dekonstruktor i mieć ich kilka w pojedynczej klasie.



### Opinia


Przyznaję, że dekonstrukcja w formie w jakiej przedstawiono ją w C#7 zupełnie mnie nie przekonuje. O ile jeszcze razem z tuplami ma to jakiś sens (jeśli przełkniemy tuple jako takie), to w połączeniu z obiektami zwykłych klas jest to opcja delikatnie zbędna. Przeglądając taki kod nie do końca będziemy w stanie wiedzieli skąd takie zmienne się wzięły, co więcej, dużo będzie tu zależeć od nazw poszczególnych parametrów w dekompozycji. Dodajmy do tego jeszcze przeciążenie dekompozycji i interpretacja takiego kodu będzie już wyzwaniem.  Nie wyobrażam sobie, aby używać tego ficzeru na co dzień, przy większych projektach. Czuję, że będzie to kolejny często &quot;banowany&quot; bajer w rozleglejszych rozwiązaniach, niczym starszy brat - klasa Tuple.



## Out variables


C# 7 uprzyjemnia także pracę z parametrami przekazywanymi z modyfikatorem  *out* . Do tej pory chcąc użyć metody z parametrami out, musieliśmy je wcześniej zadeklarować. Było to o tyle niewygodne, gdyż w większości przypadków zmienne te i tak były nadpisywane przez metody, do których były przekazywane. 


```csharp

int i;
if (int.TryParse(s, out i))
{
    Console.WriteLine($&quot;int : {i}&quot;);
}

```


Wraz z C# 7 mamy zatem możliwość zadeklarowania parametru outer w miejscu jego przekazania:


```csharp

if (int.TryParse(s, out int i))
{
    Console.WriteLine($&quot;int : {i}&quot;);
}

```


Z racji tego, że typ jest znany dla parametru outer, zamiast podawać konkretny typ, można użyć var:


```csharp

if (int.TryParse(s, out var i))
{
    Console.WriteLine($&quot;int : {i}&quot;);
}

```




### Opinia


Out variables niezmiernie przypadł mi do gustu. Rozwiązanie to jest bardzo intuicyjne i naturalne, a jednocześnie zmniejsza ilość niepotrzebnego kodu, który często był generowany przy metodach z parametrami out. Mała rzecz, ale niezmiernie cieszy. 



## Local functions


Kolejna nowość to metody lokalne. Jest to nic innego jak możliwość deklarowania funkcji na potrzeby pojedynczej metody:


```csharp

public string Multi(int dataId)
{
    return $&quot;Multiplied {MultiplyFn(2)}  {MultiplyFn(3)}&quot;;

    int MultiplyFn(int multi)
    {
        var tmp = dataId * multi;
        Console.WriteLine(tmp);
        return tmp;
    }
}

```


Warto odnotować, że w funkcji lokalnej widoczne są zmienne z metody w której została ona zadeklarowana.



### Opinia


Jest to dość kontrowersyjna opcja na dłuższą metę. Obawiam się, że dodawanie lokalnych funkcji w metodach może spowodować, że część kodu będzie dublowana. &quot;Skoro nie ma czegoś co mam obliczyć, to zapewne nikt tego nie będzie używał&quot; - takie przekonanie może doprowadzić do rozrostu lokalnych funkcji i bałaganu w kodzie. Dodatkowo jest to już jawne dawanie zielonego światła na wyrzucenie do kosza Single Responsibility Principle (SRP)...



## Return values and local variables by reference


W C# 7 postawiono również na optymalizację. Jednym z tych przykładów jest możliwość deklarowania zmiennych po referencji i zwracania wartości poprzez referencję. 


```csharp

public ref Block GetDataWithRef(ref Block
```
 data, int index) =&gt; ref data[index];

public Block GetData(ref Block[] data, int index) =&gt; data[index];

public struct Block
{
    public decimal DataBlock { get; set; }
}

public void TakeARide()
{
    Block[] data = { new Block(), new Block(), new Block() };
    ref Block dataToComputeRef = ref GetDataWithRef(ref data, 0);
    Block dataToCompute = GetData(ref data, 1);

    dataToComputeRef.DataBlock = 123; //ref, change in  data
    dataToCompute.DataBlock = 124;//copy, no change in data
}
[/code]

Dzięki zastosowaniu zwracanej referencji w metodzie  *GetDataWithRef*  unika się zbędnego kopiowania danych i operuje się na oryginalnych danych.



### Opinia


Mała drobnostka, która zapewne będzie powszechne wykorzystywana w projektach operujących na dużych strukturach danych.



## ValueTask&lt;T&gt;


C# 7 pozwoli także na optymalizację kodu asynchronicznego. Do tej pory każda metoda asynchroniczna musiała zwracać  *void* ,  *Task*  lub  *Task&lt;T&gt;*  (gdzie Task był typem refrencyjnym). Teraz ma się to zmienić i będzie można zwracać także  *ValueTask&lt;T&gt;* , typ strukturalny. 

 *ValueTask*  ma być używany w przypadku, gdy już podczas wywołania metody asynchronicznej, znana jest zwracana wartość. Użycie tej struktury ma znacząco wpłynąć na wydajność, poprzez zmniejszenie ilości alokacji na stercie.



### Opinia


Microsoft już ostrzega, iż poprawne wykorzystanie  *ValueTask&lt;T&gt;*  nie jest wcale trywialne. Użycie nowego bytu nie będzie powszechnie stosowane przez większość programistów, ale z pewnością wykorzystane zostanie w różnych zewnętrznych frameworkach i modułach. W obecnej, testowej wersji Visual Studio, nadal nie można było używać  *ValueTask* .



## Więcej expression bodied features


W C# 6 zaprezentowano metody expression bodied, które znacząco skracały pisanie jedno linijkowych metod. C# 7 dodaje możliwość skrócenia pisania konstruktorów, destruktorów oraz getterów i setterów.


```csharp

public class Vehicle
{

    public Vehicle(int fuel) =&gt; _fuel = fuel;
    ~Vehicle() =&gt; Debug.WriteLine(&quot;Finalizer called&quot;);
 
    private int _fuel;
    public int Fuel
    {
        get =&gt; _fuel;
        set =&gt; _fuel = value;
        }
    }
}

```




### Opinia


Na ten moment rozszerzone użycie expression bodied nie zostało jeszcze wprowadzone. Microsoft szczyci się, że zmiany wyszły bezpośrednio od społeczności i to ona zasugerowała twórcom te nowości. Nie jestem jednak przekonany czy faktycznie powyższy kod zyskał na czytelności, a i skrócenie go o kilka nawiasów niewiele przyspiesza w ogólnym rozrachunku. Ot taka drobnostka.



## Wyjątki w wyrażeniach


Drobnym dodatkiem jest także możliwość wyrzucania wyjątków bezpośrednio w wyrażeniach:


```csharp

public string GetUserName(string userString)
{
    return !(userString is null) ? userString.ToUpper() : 
        throw new InvalidOperationException(&quot;No user string!&quot;);
}

public string GetLoginFromDb(int id) =&gt; 
        throw new NotImplementedException(&quot;GetLoginFromDb&quot;);

```




### Opinia


Obecna wersja Visual Studio nie pozwalała na przetestowanie tej funkcjonalności. 



## Literały - usprawnienia


C# 7 dodaje także możliwość stworzenia literałów binarnych, a także rozdzielenia wpisanych wartości znakiem &quot;_&quot;, w celu ułatwienia czytelności zapisu: 


```csharp

int value1 = 0b0010_1010;
int phone = 000_000_000_111;

```




### Opinia


Taka mała drobnostka, że może nawet nie być zauważona przez większość osób. Plusem jest głównie to, że nie trzeba pamiętać wartości heksadecymalnych przy ustawianiu bitów. 



## Wildcards


Na koniec wspomnieć trzeba jeszcze o jednym ficzerze, który nie jest jeszcze w 100% potwierdzony w C#7. Mowa o wildcards.

Mając metodę, która przyjmuje parametry out:


```csharp

public void ComputeData(out int par1, out inr par2, out string par3)
{
   //...
}

```


Możemy wywołać ją z pominięciem parametrów wejściowych przy użyciu &quot;dzikiej karty&quot;, w postaci znaku &quot;*&quot;:


```csharp

ComputeData(out int par1, *)

```


Identyczne można będzie postąpić w przypadku dekonstruktorów, poniższe wywołanie:


```csharp

var (userName, userLogin, userPhone) = u;

```


zastąpić można:


```csharp

var (userName, *) = u;

```


co oznacza, iż tylko pierwszy zwracany parametr out nas interesuje.



### Opinia


Ta funkcjonalność również nie została jeszcze udostępniona... i mam nadzieję, że jej nie będzie w finalnym C#7. Jeśli połączymy wildcardy i przeciążenia w dekompozycji to otrzymamy niestrawny kotlet, który będzie nam się odbijał przez długi czas.




## Podsumowanie


C# 7 to dość kontrowersyjne zmiany. Większość nowości i usprawnień nie do końca wydaje się być bardzo przydatna. Widać tutaj, że Microsoft chce koniecznie przenieść kolejne rzeczy dostępne już w języku F# do C#. Nie wiem tylko czy jest sens wrzucanie do języka obiektowego C# elementów z funkcyjnego języka F#. W wielu miejscach C# w wersji 7 zaczyna przypominać zmiany w JS z ECMAScript 6, co nie do końca jest będzie się podobać.

Przy kilu drobnych, ale przydatnych ficzerach jak out variables czy pattern matching są bardzo dyskusyjne nowości. Wspomnę tylko o nowych tuplach, dekompozycji czy funkcjach lokalnych. O ile ostatnie iteracje C# oferowały zawsze jakieś ciekawe zmiany (C# 5 - async/await, C# 6 - Elvis) to C# 7 jest dość kontrowersyjny. 

Oczywiście nie jest to nadal wersja finalna, ale można przyjąć, że niezbyt wiele się tutaj zmieni. Ogólnie jestem trochę zawiedziony C# 7, a nawet zdegustowany kilkoma zaproponowanymi elementami.

Postęp prac nad C# 7 można obserwować na [GitHubie](https://github.com/dotnet/roslyn/blob/master/docs/Language%20Feature%20Status.md). Link do blogu na [MSDN](https://blogs.msdn.microsoft.com/dotnet/2016/08/24/whats-new-in-csharp-7-0/).)