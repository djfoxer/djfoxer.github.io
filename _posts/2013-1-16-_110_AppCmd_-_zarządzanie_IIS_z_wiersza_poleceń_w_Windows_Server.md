---
layout:     post
title:      AppCmd - zarządzanie IIS z wiersza poleceń w Windows Server
date:       2013-01-16 19:48:00
summary:    Zarządzanie usługami IIS z poziomu GUI jest dziecinnie proste. Od wersji 7.0 wszystkie opcje są łatwo dostępne i zarządzanie jest niezmiernie proste. Oczywiście interfejs graficzny nie zawsze jest wygody w pewnych zastosowaniach. Do napisania skryptu zarządzającego witryną czy pulą aplikacji łatwiej...
categories: windows oprogramowanie serwery
---



Zarządzanie usługami IIS z poziomu GUI jest dziecinnie proste. Od wersji 7.0 wszystkie opcje są łatwo dostępne i zarządzanie jest niezmiernie proste. Oczywiście interfejs graficzny nie zawsze jest wygody w pewnych zastosowaniach. Do napisania skryptu zarządzającego witryną czy pulą aplikacji łatwiej użyć oczywiście wiersza poleceń. W tym momencie z pomocą przychodzi narzędzie AppCmd - administracja IIS z poziomu konsoli bez użycia graficznego środowiska Menadżera.

AppCmd pozwala na na:


  * Tworzenie i konfigurowanie witryn, pól aplikacji, katalogów wirtualnych


  * Zatrzymywanie i wznawianie witryn


  * Zatrzymywanie, wznawianie i  odtwarzanie pól aplikacji


  * Podgląd procesów


  * Analiza reqestów aplikacji na serwerze IIS


  * Zarządzanie i backup konfiguracji aplikacji


  * Mechanizm potoków


AppCmd.exe znajduje się w folderze  *%windir%\system32\inetsrv* . Powyższa ścieżka nie istnieje w zmiennej  *path* , a zatem aby ułatwić pracę, można ją tam dopisać. Dzięki temu zabiegowi uzyskamy dostęp do aplikacji z każdej lokacji.



## Składnia


Narzędzie AppCmd działa poprzez wydanie odpowiednich poleceń ( *command* ) dla obiektów ( *object-type* ) z opcjonalnymi parametrami ( *parameter1:value1 ...* ):


```shell
appcmd (command) (object-type) <identifier> </parameter1:value1 ...>
```


Obiektem może być:  SITE, APP, VDIR, APPPOOL, CONFIG, WP, REQUEST, MODULE, BACKUP, TRACE. W zależności od wybranego obiektu, posiada on własną listę komend, jaką można użyć. Najłatwiej przejrzeć ją poprzez zapytanie:


```shell
appcmd (object-type) /?
```


O parametrach do komend, najszybciej dowiemy się poprzez polecenie:


```shell
appcmd (command) (object-type) /? 
```





## Przykłady



Teoria już za nami. Przejdźmy do kilku przykładów które pokarzą możliwości AppCmd, a także najbardziej przydatne polecenia. Część poleceń  np.  *delete* , czy  *set* , jest analogiczna dla większości obiektów i nie ma potrzeby powtarzania ich dla każdej z opcji.



### Witryny





  * lista witryn


```shell
appcmd list sites
```

Jeśli dodamy np. parametr  */state:Started* , otrzymamy listę z tylko aktywnymi witrynami. Listę możemy filtrować również za pomocą innych parametrów (patrz następny podpunkt).


  * dodanie witryny


```shell
appcmd add site /name:Test /id:10 /bindings:"http/*:95:" /physicalPath:"c:\PUB\d1" 
```

 *name*  - nazwa witryny,  *id*  - identyfikator witryny,  *bindings*  - powiązania (w tym przypadku dostęp przez port 95)


  * zmiana parametrów


```shell
appcmd set site Test /id:20 
```




  * usuwanie


```shell
appcmd delete site Test
```






### Aplikacje


Mając już witrynę możemy pobawić się z aplikacjami w jej obrębie.



  * dodanie aplikacji



```shell
appcmd add app /site.name:Test /path:/a1 /physicalPath:"c:\PUB\d1\a1"
```

 *site.name*  - witryna,  *path*  - ścieżka wirtualna (w tym przypadku będzie to a1, czyli dostęp będzie poprzez adres:  *http://adres:95/a1* ),  *physicalPath*  - ścieżka fizyczna do folderu z plikami




### Pule aplikacji





  * 


  * dodanie puli aplikacji


```shell
appcmd add apppool /name:apool
```

Dodaliśmy własną pulę aplikacji o nazwie  *apool* .

  * podgląd puli aplikacji


```shell
appcmd list apppool "apool" /text:*
```

Na wyjściu otrzymamy podgląd konfiguracji puli aplikacji:


```txt

APPPOOL
  APPPOOL.NAME:"apool"
  PipelineMode:"Integrated"
  RuntimeVersion:"v4.0"
  state:"Started"
  [add] 
    name:"apool" 
    queueLength:"1000" 
    autoStart:"true" 
    enable32BitAppOnWin64:"false" 
    managedRuntimeVersion:"v4.0" 
(...)

```



  * edycja

Dowolny parametr edytujemy w następujący sposób:

```shell
appcmd set apppool "apool" /autoStart:"false"
```






### Foldery wirtualne





  * tworzenie folderu


```shell
appcmdadd vdir /app.name:"Test/a1" /path:/a2 /physicalPath:"c:\PUB\d1\a2"
```


Powyższe polecenie w naszym przypadku utworzyło wirtualną ścieżkę dla  *Test/a1* .


  * listowanie


```shell
appcmd list vdir /physicalPath:"c:\PUB"
```

Pomimo, iż listowanie, w każdym przypadku wygląda podobnie, to dzięki parametrom, można odfiltrować dane wg potrzeb. Tutaj tylko te witryny, które znajdują się fizycznie, w określonym folderze.





### Backup


Dzięki appcmd w prost sposób wykonany backup konfiguracji serwera:


  * backup


```shell
appcmd add backup "b20120116"
```


  * przywrócenie kopii


```shell
appcmd restore backup "b20120116"
```






### Procesy





  * analiza procesów

Obiekt  *wp*  pozwala w prosty sposób na podgląda działających procesów. Poniższe polecenia listują wszystkie procesy działające na domyślnej puli aplikacji:

```shell
appcmd list wps /apppool.name:DefaultAppPool
```

lub dziłające na okreslonym numerze PID:

```shell
appcmd list wp "35674"
```






### Śledzenie witryn


Ciekawym obiektem jest  *trace*  to śledzenia witryn. Można w prosty sposób przeanalizować działanie witryn pod kątem błędów.


  * dodanie witryny do śledzenia


```shell
appcmd configure trace "Test" /enablesite
```

Dodaliśmy śledzenie dla witryny  *Test* .

  * podgląd logu

Aby podejrzeć działanie  *trace* , na początku należy wylistować logi (pliki XML):

```shell
appcmd list traces
```

Z logów wybieramy ten, który nas interesuje i wyświetlamy go

```shell
appcmd list trace "id_logu.xml" /text:path
```





### Potoki


Dzięki zaimplementowanemu mechanizmowi potoków, można jeszcze więcej wycisnąć z appcmd. Oto kilka bardziej zaawansowanych przykładów, które wykorzystują potoki (dla ułatwienia analizy, dodałem linie nowych znaków pomiędzy potokami):



  * szybkie uruchomianie nieaktywnych witryn


```shell
appcmd list site /state:stopped /xml 
| appcmd start site /in
```

Listujemy witryny nieaktywne (wyjście w formacie  */xml* ) i wrzucamy je jako wejście ( */in* ) do polecenia uruchomienia witryn.

  * recycling puli aplikacji, dla witryn które generują błąd 500



```shell
appcm list trace /statusCode:500 /xml 
| appcmd list apppool /in /xml 
| appcmd recycle apppool /in
```


W tym przypadku listujemy witryny, generujące błąd 500, następnie przekazujemy je do  *list apppool*  w celu uzyskania odpowiednich pól aplikacji i na koniec robimy recycling tych puli.





## Podsumowanie


AppCmd to potężne narzędzie do zarządzania IIS z konsoli, w przypadku gdy np. nie możemy skorzystać z graficznego odpowiednika. Przedstawiłem zaledwie kilak podstawowych i najprzydatniejszych funkcji. Jeszcze jest wiele do odkrycia. Cieszy duża gama opcji i co najważniejsze, mechanizm potoków, który jest tu wręcz niezbędny.