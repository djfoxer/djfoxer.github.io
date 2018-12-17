---
layout:     post
title:      Zapisywanie zdarzeń z wtyczki do Visual Studio w Activity Logu
date:       2017-05-22 23:57:00
summary:    Dzisiejszy wpis odnośnie tworzenia wtyczki do Visual Studio będzie bardzo szybki i konkretny. W każdej aplikacji przychodzi moment na to, aby zalogować do pliku jakieś zdarzenie. Może być to notka o wyłapanym wyjątku,  bądź też tylko zapis czysto informacyjny. <!----><!---->Zapis w Activity LogDodatki do IDE od Microsoftu mogą zapisywać zdarzenia do Activity Loga. W celu umieszczenia własnego wpis...
categories: windows porady programowanie
slug: Zapisywanie-zdarzen-z-wtyczki-do-Visual-Studio-w-Activity-Logu,81198.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-22-_20_/g_-_-x-_-_-_x20170522234622_0.png
---



Dzisiejszy wpis odnośnie tworzenia wtyczki do Visual Studio będzie bardzo szybki i konkretny. W każdej aplikacji przychodzi moment na to, aby zalogować do pliku jakieś zdarzenie. Może być to notka o wyłapanym wyjątku,  bądź też tylko zapis czysto informacyjny. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-22-_20_/g_-_-x-_-_-_x20170522234622_0.png)





### Zapis w Activity Log




Dodatki do IDE od Microsoftu mogą zapisywać zdarzenia do Activity Loga. W celu umieszczenia własnego wpisu należy pobrać serwis o typie  *SVsActivityLog*  i rzutować go na interfejs IVsActivityLog:



```csharp

var log = serviceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;


```

 

gdzie  *serviceProvider*  jest obiektem dziedziczącym po  *IServiceProvider*  (w naszym przypadku jest to obiekt klasy  *Package* ).

Logowanie odbywa się przy pomocy metody  *LogEntry* :



```csharp

log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_ERROR, pluginName, message);

```



Pierwszy parametr określa poziom logowania - jest nim enumerator __ACTIVITYLOG_ENTRYTYPE i posiada od trzy wartości: błąd (ALE_ERROR), ostrzeżenie (ALE_WARNING) i informacja (ALE_INFORMATION). Drugi parametr opisuje źródło logu, zaś trzeci parametr jest tekstowym opisem loga.



### Aktywacja i przeglądanie logów


Logi składowane są przez IDE domyślnie w pliku  *ActivityLog.xml* , który znajduje się w folderze  *%AppData%\Microsoft\VisualStudio\[Numer_wersji_VS]\* . Pamiętać należy, że dopiero uruchomienie Visual Studio z przełącznikiem  */log* , aktywuje zapis do Activity Loga. Dodatkowo można zmienić miejsca zapisu, poprzez dodanie ścieżki: /log  *c:\users\user\desktop\activitylog.xml* 





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-22-_20_/g_-_-x-_-_-_x20170522234628_1.PNG)



Jest to idealny sposób na analizę działania IDE w przypadku, gdy mamy problemy ze stabilnością Visual Studio. Zapis logów z własnej wtyczki pomoże na pewno w rozwiązaniu błędów u użytkowników końcowych. Wynikowy plik jest typu XML, który dodatkowo związany jest z plikiem ActivityLog.xsl, będącym zasobnikiem na szablon styli.  ActivityLog powinien zostać automatycznie otworzony przez przeglądarkę IE lub inny domyślny program do podglądu plików XML.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-5-22-_20_/g_-_-x-_-_-_x20170522234628_0.PNG)



