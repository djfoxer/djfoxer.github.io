---
layout:     post
title:      Simple.Data - rewelacyjna biblioteka .NET ORM bez ORMa!
date:       2012-11-13 13:44:00
summary:    W tym wpisie pragnę przedstawić krótkie wprowadzenie do genialnej w swojej prostocie biblioteki Simple.Data dla platformy .NET. Otóż zapewne każdy kto miał styczność z programowaniem, musiał w pewnym momencie skorzystać z bazy danych. Wówczas najczęściej pada wybór na Entity Framework lub (Fluent) nHibernate jako framework ORM.  Pociąga to za sobą tworzenie obiektów (Object), posiadanie relacyjnej...
categories: porady programowanie
slug: SimpleData-rewelacyjna-biblioteka-NET-ORM-bez-ORMa,37175.html
---



W tym wpisie pragnę przedstawić krótkie wprowadzenie do genialnej w swojej prostocie biblioteki Simple.Data dla platformy .NET. 



Otóż zapewne każdy kto miał styczność z programowaniem, musiał w pewnym momencie skorzystać z bazy danych. Wówczas najczęściej pada wybór na Entity Framework lub (Fluent) nHibernate jako framework [ORM](http://en.wikipedia.org/wiki/Object-relational_mapping).  Pociąga to za sobą tworzenie obiektów ( *Object* ), posiadanie relacyjnej bazy danych ( *Relational* ), a także stworzenie relacji ( *Mapping* ). Oczywiście każdy z tych frameworków posiada generator dla obiektów i relacji. Jednakże pomimo tych udogodnień, stworzenie ich wymaga zawsze poświęcenia czasu. Co więcej, jeśli baza nie jest budowana razem z projektem, a opiera się już na istniejącej, wówczas wymaga to jeszcze więcej pracy. Każda z bibliotek jest bardzo wrażliwa na wszelkie niestandardowe rozwiązania lub nieścisłości. Te zaś występują często w istniejących już bazach, które współdzielone są przez kilka aplikacji. Jakakolwiek zmiana w takim przypadku nie wchodzi w rachubę. Odpowiednie skonfigurowanie wszystkiego, aby później nie sprawiało już problemów, jest pracochłonne. 

Jeśli nasz projekt korzysta z bazy danych okazjonalnie i/lub nie wymaga niesamowitych skomplikowanych operacji, wówczas wdrożenie Entity Framework lub (Fluent) nHibernate nie jest zbyt opłacalne. Szczególnie, gdy z wielu istniejących tabel, mających wiele relacji, będziemy używać zaledwie kilku. W tym momencie idealnym rozwiązaniem jest [Simple.Data](http://simplefx.org/simpledata/docs/index.html) !



## Simple.Data - ORM bez ORMa




[Simple.Data](http://simplefx.org/simpledata/docs/index.html)  jest lekkim frameworkiem dla .NET, który zapewnia dostęp do bazy w stylu ORM, ale bez obiektów ( *Object* ), bez wymogu łączenia się do relacyjnej bazy danych ( *Relational* ) a także bez generowania relacji ( *Mapping* )! Wszystko dzięki typom dynamicznym w .NET 4!

Simple.Data posiada adaptery do:


  * ADO.NET obsługuje następujące bazy:


  * SQL Server 2005 i nowsze

  * SQL Server Compact Edition 4.0

  * Oracle

  * VistaDB

  * MySQL 4.0 i nowsze

  * SQLite 3.0 i nowsze

  * PostgreSQL

  * SQLAnywhere

  * Informix



  * MongoDB

  * OData

  * Azure



### Wymagania i konfiguracja



Dla platformy .NET wymagana jest wersja 4 lub wyższya, zaś jeśli chcemy używać Simple.Data z Mono, musimy posiadać wersję co najmniej 2.1. Aktualna wersja znajduje się na [githubie](https://github.com/markrendle/Simple.Data),  ale najprościej pobrać ją poprzez [NuGeta](http://nuget.codeplex.com/).  

Zawsze do poprawnego działania wymagana jest biblioteka  *Simple.Data.Core*  oraz biblioteka Simple.Data dla konkretnego adaptera ( *ADO.NET, MongoDB, OData, Azure* ). Wybierając adapter  *ADO.NET*  należy dołożyć jeszcze bibliotekę Simple.Data dla konkretnej bazy, z jaką będziemy działać.

Jedynie co należy skonfigurować to... connection string. Można trzymać go zarówno w pliku  *.config* , jak i podać jako argument przy otwieraniu połączenia z bazą danych. Oczywiście nie ma ograniczenia do ilości połączeń. Tutaj mała uwaga, Simple.Data nie utrzymuje połączenia, a zatem obiekt zwrócony z  *Database.Open()*  można przetrzymywać w singletonie, jeśli jest taka potrzeba. Gdy specyfikacja projektu nie pozwoliłaby na to, nic nie stoi na przeszkodzie, aby samemu zarządzać kiedy następuję połączenie/rozłączenie ([szczegóły](http://simplefx.org/simpledata/docs/pages/Start/SharingAConnection.html) ).



### Jak to działa?


Otóż język .NET 4 wprowadził m.in. dynamiczne typy. Simple.Data wykorzystuje to w sprytny sposób. Korzystając z kilkudziesięciu zdefiniowanych metod i łącząc je z z tym, co chcemy pobrać z bazy, uzyskujemy bardzo prosty i szybki framework. Poniżej kilka przykładów przedstawiających Simple.Data. Dzięki nim łatwiej będzie zrozumieć, jak ta biblioteka świetnie nadaje się do małych i średnich projektów, które nie wymagają zaprzęgania wielkich frameworków ORM.



### Prosty przykład



Nadeszła pora, aby pokazać jak to działa w praktyce. Dzięki czemu można uzmysłowić sobie jak szybkim i elastycznym frameworkiem jest Simple.Data. Oto "książkowy" przykład, jak robimy to w standardowy, klasyczny sposób:



```javascript

public Book FindBookById(int id)
{
    Book book = null;
    using (var connection = new SqlConnection(ConfigurationManager
    .ConnectionStrings["Default"].ConnectionString))
    using (var command =
    new SqlCommand("SELECT [Id],[WriterId],[Name],[Year]"+
    "FROM [Book] where id= @id", connection))
    {
        command.Parameters.Add("@id", SqlDbType.Int).Value = id;
        connection.Open();
        using (var reader = command.ExecuteReader())
        {
            if (reader.Read())
            {
                book = new Book {
                    Id = reader.GetInt32(0), WriterId = reader.GetString(1),
                Name = reader.GetString(2), Year = reader.GetString(3) };
            }
        }
    }
    return book;
}

```



a teraz to samo, ale z Simple.Data (bez generowania czegokolwiek!):



```javascript

public Book FindBookById(int id)
{
    return Database.Open().Books.FindAllById(id).FirstOrDefault();
}

```



czy jeszcze prościej bez żadnych klas:



```javascript

var book =  Database.Open().FindAllById(2).FirstOrDefault();

```



Jak to działa na powyższym przykładzie?



  *  *Database.Open()*  - w tym miejscu nawiązywane jest połączenie. Metoda  *Open*  bez parametru, pobiera domyślny connection string z configu i zwraca łącznik bazy. Co ciekawe Database jest jedynym niedynamicznym obiektem. 


  *  *Books*  - domyślnie kolejnym elementem jest nazwa tabeli/widoku. Liczba pojedyncza/mnoga nie ma znaczenia. Czy użyjemy Book, czy Books, Simple.Data i tak stworzy poprawny zapytanie. W powyższym przykładzie - Books - spowoduje, iż framework stworzy kilka możliwych wersji (Books, books, book) i spróbuje znaleźć pasującą nazwę w  *INFORMATION_SCHEMA.TABLES*   


  *  *FindAllById*   - ten wyrażenie to połączenie kilku elementów. Metody: [FindAllBy](http://simplefx.org/simpledata/docs/pages/Retrieve/Commands/FindAllBy.html),  która oznacza, iż chcemy pobrać rekordy o zadanym, co najmniej jednym warunku. W tym przypadku jest to  *Id* . Oczywiście można dodawać ich więcej np.  *FindAllByYearAndWriterId("2011", 1)* . Warto dodać, że istnieje również alternatywna metoda tworzenia zapytań np.  *FindAllBy(Year: "2011", WriterId: 1)*  (dla niektórych bardziej czytelne).  


Tak naprawdę to tylko tyle ;) Wygenerowany w taki sposób kod SQL wygląda następująco:

```sql

SELECT [dbo].[book].[id], 
       [dbo].[book].[writerid], 
       [dbo].[book].[name], 
       [dbo].[book].[year], 
       [dbo].[book].[description] 
FROM   [dbo].[book] 
WHERE  [dbo].[book].[id] = @p1 

(@p1 (Int32) = 2)

```





### Coś trudniejszego - JOIN



Powyższy przykład był dość prosty, teraz coś ciekawszego: JOIN. Otóż w Simple.Data jest to równie trywialne. Rozpatrzmy jednak dwa przypadki. 




  * istnieją odpowiednie klucze obce w tabelach





```javascript

var db = Database.Open();

var books = db.Books.FindAllByYear("2011")
    .Select(
db.Books.Name,
db.Books.Writer.FirstName);

```



W tym przypadku pobieramy wszystkie książki (Books) z roku 2011, łącząc przy okazji z autorem książki (Writer). Dodatkowo, dzięki [Select](http://simplefx.org/simpledata/docs/pages/Retrieve/ColumnSelection.html),  można było wybrać, które kolumny mają być zwrócone. Wszystkie kolumny można wybrać używając metody Star().



```sql

SELECT [dbo].[book].[name], 
       [dbo].[writer].[firstname] 
FROM   [dbo].[book] 
       LEFT JOIN [dbo].[writer] 
              ON ( [dbo].[writer].[id] = [dbo].[book].[writerid] ) 
WHERE  [dbo].[book].[year] = @p1 

(@p1 (String) = 2011)

```



Przypominam - automatyczne połączenie JOIN może powstać, gdy odpowiednio oznaczone są klucze obce w tabelach. 




  * brak kluczy obcych





```javascript

var db = Database.Open();

var books = db.Books.FindAllByYear("2011")
    .Select(
db.Books.Name,
db.Books.Writer.FirstName)
    .LeftJoin(db.Writer).On(db.Writer.Id == db.Books.WriterId);

```



Ja widać, [LeftJoin](http://simplefx.org/simpledata/docs/pages/Retrieve/LazyLoadingJoins.htm)  pozwala na połączenie tabel, które nie mają założonych kluczy obcych. W ten prosty sposób można połączyć dwie tabele po odpowiednich kolumnach.

Wygenerowany kod przedstawia się następująco:



```sql

SELECT [dbo].[book].[name], 
       [dbo].[writer].[firstname] 
FROM   [dbo].[book] 
       LEFT JOIN [dbo].[writer] 
              ON ( [dbo].[writer].[id] = [dbo].[book].[writerid] ) 
WHERE  [dbo].[book].[year] = @p1 
@p1 (String) = 2011

```





### Poziom wyższy - stronicowanie



Tera coś ciekawszego, co może przydać się często w przypadku tworzenia małych CRMów. Otóż jak wyglądać będzie pobieranie danych ze stronicowaniem (idealne do grida)? Simple.Data i w tym przypadku zaskakuje, pozytywnie!

Aby nie komplikować kodu załóżmy, że chcemy robić stronicowanie tabeli z książkami (Books). Oczywiście ma pojawiać się również ogólna ilość rekordów i opcja sortowania. Napisanie tego w SQL wymaga trochę klepania. Jak wygląda to w Simple.Data? Trzymajcie się ;)



```javascript

var db = Database.Open();
Future < int > count;

var books = db.Books.All()
    .OrderByDescending(db.Books.Name)
    .WithTotalCount(out count)
    .Skip(5)
    .Take(2)
    .ToList();

```



Czyż to nie jest proste? Cóż ten wielce skomplikowany kod robi :) Dla tabeli Book brane są wszystkie rekordy ( *All* ). Następnie zostają one posortowane ( *OrderByDescending* ) po nazwie. Stronicowanie załatwiają dwie metody:  *Skip*  i  *Take* . Pierwsza przeskakuje o zadaną ilość rekordów, a druga pobiera dokładnie tyle elementów, ile chcemy. Piękne.

Jak wygląda wygenerowany kod SQL?



```sql

SELECT Count(*) 
FROM   [dbo].[book]; 

WITH __data 
     AS (SELECT [dbo].[book].[id], 
                [dbo].[book].[writerid], 
                [dbo].[book].[name], 
                [dbo].[book].[year], 
                [dbo].[book].[description], 
                Row_number() 
                  OVER( 
                    ORDER BY [dbo].[book].[name] DESC) AS [_#_] 
         FROM   [dbo].[book]) 
SELECT [id], 
       [writerid], 
       [name], 
       [year], 
       [description] 
FROM   __data 
WHERE  [_#_] BETWEEN 6 AND 7 

```



Jak dla mnie, jak najbardziej poprawnie i do zaakceptowania. A robi to taki mały kawałeczek kodu!




## Simple.Data - szybkość i prostota



Przedstawiłem zaledwie mały wycinek funkcjonalności jakie posiada Simple.Data. Nie pisałem o tak trywialnych rzeczach jak dodawanie, aktualizowanie, usuwanie rekordów. Biblioteka oferuje również wsparcie dla testów jednostkowych, czy nawet wykonywanie procedur (przypominam sobie zabawy z nimi w Fluent nHibernate)! Więcej możliwości znajdziemy w [dokumentacji](http://simplefx.org/simpledata/docs/),  która nie zawsze jest aktualizowana, po najnowsze zmiany i nowinki polecam gorąco, zajrzeć na [ blog autora](http://blog.markrendle.net/).  

Simple.Data jest genialnym, niewielkim  i szybkim  frameworkiem do małych i średnich
 projektów. Pomimo prostoty, posiada bogatą funkcjonalność, a ilość obsługiwanych typów baz, zachwyca. Nie ma oczywiście "róży bez ognia". Całkowita dynamiczność wiąże za sobą brak jakiegokolwiek intellisense. Musimy pamiętać każdą z metod i parametrów. Oczywiście prostota frameworku pozwala nieznacznie przełknąć tą niedogodność. Następny problem również zahacza o dynamiczność. Brak klas reprezentujących tabele, powoduje to iż jakakolwiek zmiana w bazie (zmiana nazwy kolumny, usunięcie kolumny) nie spowoduje błędu kompilacji. Dowiemy się jednak dopiero podczas działania aplikacji albo wcale! Dlatego Simple.Data polecam do maksymalnie średnich projektów, by nie złapać się na tego typu niuanse. Co nie zmienia faktu, iż framework ma ogromne zastosowania i gorąco polecam do zapoznania się z nim!