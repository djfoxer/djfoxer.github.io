---
layout:     post
title:      Nowości w C# 6 — cóż ciekawego otrzymujemy?
date:       2016-07-18 18:57:00
summary:    Tak, tak, tak. C# 6 jest już z nami od jakiegoś już czasu, ale w życiu nie jest tak kolorowo i nie wszyscy mogli przejść na nowego Visual Studio 2015 tuż po tym jak się ukazał. Dodatkowo nawet jeśli ktoś już przesiadł się na najświeższe IDE od MS, to i tak nie zawsze mógł używać nowości, które wpadły wraz z C# 6. Zatem dla niektórych będzie to przypomnienie, dla innych zapoznanie się z nowościami....
categories: windows programowanie
slug: Nowosci-w-C-6-coz-ciekawego-otrzymujemy,74772.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-7-18-_47_/g_-_-x-_-_-_x20160716023110_0.jpg
---



Tak, tak, tak. C# 6 jest już z nami od jakiegoś już czasu, ale w życiu nie jest tak kolorowo i nie wszyscy mogli przejść na nowego Visual Studio 2015 tuż po tym jak się ukazał. Dodatkowo nawet jeśli ktoś już przesiadł się na najświeższe IDE od MS, to i tak nie zawsze mógł używać nowości, które wpadły wraz z C# 6. 

Zatem dla niektórych będzie to przypomnienie, dla innych zapoznanie się z nowościami. Co więcej, w sieci jest wiele stron opisujących nowe elementy w C#, które... nie znalazły się w finalnym wydaniu.

Sam C# 6 nie przynosi olbrzymich zmian czy nowości. W tym wydaniu nastawiono się głównie na wprowadzenie małych ficzerów, które uprzyjemnią pracę z kodem i zmniejszą jego ilość, zwiększając przy tym czytelność.

Cóż ciekawego pojawi się zatem w wraz z C# 6?



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-7-18-_47_/g_-_-x-_-_-_x20160716023110_0.jpg)





### Operator  *?.* 

 
To chyba jedna z bardziej wyczekiwanych nowości w C# 6. Zmorą deweloperów tworzących w C# jest wyjątek  *NullReferenceException* . Powoduje to często, że kod w wielu miejscach złożony jest if-ów, w których sprawdzamy czy coś nie jest nullem.

 *Klasycznie:* 


```csharp

if (client != null &&
    client.Baskets != null &&
    client.Baskets.Any(x => x.Items != null && x.Items.Length > 1))
{
    Console.WriteLine("OK!");
}

```



Od teraz możemy zastąpić sprawdzanie czy zmienna nie jest nullem poprzez użycie operatora  *?.*  zwanego potocznie Elvis operatorem (przekręćcie głowę, aby zobaczyć Króla RnR)

 *C# 6:* 


```csharp

if (client?.Baskets?.Any(x => x.Items?.Length > 0) ?? false)
{
    Console.WriteLine("OK!");
}

```



Warto odnotować, że używając operatora możemy uprzyjemnić sobie życie z delegatami.

Do tej pory jeśli chcieliśmy odpalić delagat, dbając o wątki, należało zrobić to w następujący sposób:



```csharp

var onChanged = OnChanged;
if (onChanged != null)
{
    onChanged(this, args);
}

```



Za pomocą  *?.*  ten sam kod (thread-safe) w C# 6 napiszemy:



```csharp

OnChanged?.Invoke(this, args);

```





### Właściwości - inicjalizacja



Możemy już inicjalizować właściwości, podobnie jak w przypadku pól:



```csharp

public class Customer
{
    public string First { get; set; } = "Jon";
    public string Last { get; set; } = "Snow";
}

```



Warto dodać, że inicjalizacja nie przebiega poprzez  *set* , ale wartość jest  nadawana bezpośrednio. 



### Właściwości -  *readonly* 




```csharp

public class Customer
{
    public string First { get; } = "Jon";
    public string Last { get; }

    public Customer(string last)
    {
        Last = last;
    }
}

```



Właściwości można od teraz tworzyć bez użycia settera. W takim wypadku niejawnie tworzone jest pole  *readonly* . Właściwość może być znacjonalizowana tylko bezpośrednio (jak wyżej) lub w konstruktorze.



### String interpolation


Kolejną ciekawią nowością jest interpolacja Stringów. Zamiast używać  *String.Format*  możemy to samo zrobić w znacznie krótszy sposób:




```csharp

string first = "Jon", last = "Snow";

var s_old = String.Format("{0} likes {1}", first, last);

var s_csharp6 = $"{first} likes {last} now {DateTime.Now:d}";

```






### Metody, właściwości i indeksatory jako pojedyncze wyrażenie lambda



W C# 6 dostaliśmy możliwość zapisywania metod, będących pojedynczymi wyrażeniami, w prostej i zwięzłej formule. Oczywiście metody takie mogą również zwracać  *void* .

 *Klasycznie:* 


```csharp

public decimal AddMoney(decimal toAdd)
{
    return Money += toAdd;
}

```



 *C# 6:* 


```csharp

public decimal AddMoney(decimal toAdd) => Money += toAdd;

```



Funkcjonalność ta została rozszerzona także o właściwości i indeksatory. W przypadku tych pierwszych tworzymy wyliczanlne właściwości (tylko do odczytu).


 *Klasycznie:* 


```csharp

public string FullName
{
    get
    {
        return First + " " + Last;
    }
}

```



 *C# 6:* 


```csharp

public string FullName => First + " " + Last;

```



W ten sposób otrzymujemy znacznie  *lżejszy*  kod od strony wizualnej. Czytelność jest już jednak miejscami dyskusyjna.



```csharp

public class Customer
{
    public string First { get; } = "Jon";
    public string Last { get; } = "Snow";
    public decimal Money { get; set; } = 100;
    private string[] values = new string[100];
    
    //metody
    public decimal AddMoney(decimal toAdd) => Money += toAdd;
    public void Print() => Console.WriteLine(FullName);
    //właściwości 
    public string FullName => First + " " + Last;
    //indeksator
    public string this[long id] => id >= 0 && id < values.Length ? values[id] : null;

}

```











### Using static


W najnowszej wersji C# możemy korzystać z fleczeru, który pozwala na używanie dostępnych statycznych elementów w klasach czy Enumach.

 *Klasycznie:* 


```csharp

class Program
{
    static void Main()
    {
        Console.WriteLine(Math.Sqrt(10));
        Console.WriteLine(DayOfWeek.Friday - DayOfWeek.Monday);
    }
}

```


 *C# 6:* 


```csharp

using static System.Console;
using static System.Math;
using static System.DayOfWeek;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(10)); 
        WriteLine(Friday - Monday); 
    }
}

```





W ten sposób można jednak łatwo skomplikować sobie życie.


> Pytanie: czy  *Sqrt(10* ) przejdzie do metody z klasy  *System.Math*  czy  *Program* , a może wyskoczy wyjątek przy kompilacji?




```csharp

using static System.Console;
using static System.Math;
using static System.DayOfWeek;

class Program
{
    static void Main()
    {
        WriteLine(Sqrt(10));
        WriteLine(Friday - Monday);
    }

    int Sqrt(int x)
    {
        return x - 3;
    }
}

```



Ficzer całkiem ciekawy. Z jednej strony zmniejsza ilość kodu i poprawia jego czytelność, ale z drugiej może wprowadzać pewnie niejasności w zrozumieniu kontekstu.  *Using static*  zapewne najlepiej nada się do użycia dla kilku ściśle wybranych klas, aby nie utrudnić analizy kodu.



###  *nameof* 


C# 6 wprowadza również wyrażenie  *nameof* , które zwraca stringa będącego nazwą zmiennej, właściwości, klasy czy metody:



```csharp

return nameof(var1) //"var1"

return nameof(collection.Item.Index) //"Index"

```


Idealnie nada się do wywołania  *PropertyChanged* , wyrzucania wyjątków z informacją o nazwie zmiennej, czy operując na typach generycznych



```csharp

if (value== null) throw new ArgumentNullException(nameof(value)+ " is null :(");

```





### Filtrowanie wyjątków



W nowej wersji języka dostaliśmy możliwość dodawania filtrów do wyjątków:



```csharp

try
{
	throw new Exception("My exception");
}
catch (Exception ex) when (ex.Message == "My exception")
{
	Console.WriteLine("My exception caught");
}
catch (Exception ex) 
{
	Console.WriteLine("Other exception caught here");
}

```





### Pozostałe zmiany:





  * nowe, bardziej przyjazne inicjalizery do słowników:

 *Klasycznie:* 


```csharp

var dic = new Dictionary<string, int> {
    {"x", 1},
    {"y", 2}
};

```


 *C# 6:* 


```csharp

var dic = new Dictionary<string, int> {
    ["x"] = "1",
    ["y"] = "2",
};

```





  *  *await*  w  *catch*  i  *finally* 

C# 6 pozwala już na używanie  *await*  w blokach  *catch*  i  *finally* . Podobno Microsoft użył sporej dawki magii, aby to zaimplementować (na początku twierdzili, że się nie da), ale finalnie udało się:



```csharp

try
{
    …
} 
catch(Exception e)
{
    await LogAsync(e); 
}
finally
{
    await Close();
}

```







  * stworzone  *Extension method*   *Add*  w kolekcji zostanie użyte przy inicjalizacji kolekcji:



```csharp

namespace MyExtensions
{
    public static class DicExt
    {
        public static void Add(this Dictionary<string, int> dic, int value)
        {
            dic.Add("Number " + no.ToString(), value);
        }
    }
}

using MyExtensions

var dic = new Dictionary<string, int> { 1, 4, 10 };


```





  * do numerów z błędami w  *#pragma warning disable/restore*  doszedł opcjonalny prefix "CS"  

  * usprawniono mechanizm przeciążeń




To tyle :) Nie wszystkie zmiany są szczególnie ciekawe, a kilka z nich może nawet delikatnie utrudnić późniejszą analizę kodu, jeśli będą używane w nadmiarze i w niewłaściwy sposób.  *Metody, właściwości i indeksatory jako pojedyncze wyrażenie lambda*  - tutaj jeśli za dużo zechcemy upchać do wyrażeń, wówczas otrzymamy jednolinijkowe potwory. W przypadku  * using static*  trzeba uważać na to, aby niechcący nie pomieszać kontekstów, co innego że ficzer jest racze zbędnym bajerem w codziennym kodowaniu.

Ogólnie warto jednak odnotować, że pojawił się nareszcie  *Elvis* , który zapewne będzie często używany przez programistów. Również zmiany we właściwościach są ciekawą opcją, podobnie jak  *nameof*  i interpolacja stringów. Pozostałe rzeczy są raczej małymi ułatwieniami, których możemy nawet nie zauważyć. 