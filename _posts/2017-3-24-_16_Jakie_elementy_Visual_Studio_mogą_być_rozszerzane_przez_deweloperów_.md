---
layout:     post
title:      Jakie elementy Visual Studio mogą być rozszerzane przez deweloperów?
date:       2017-03-24 17:36:00
summary:    IDE od Microsoftu pozwala na rozszerzenie możliwości środowiska programistycznego za pomocą wtyczek. Do jakich elementów Visual Studio można tworzyć wtyczki? W skrócie można napisać, że niemalże każda część składowa IDE jest podatna na rozbudowanie. Przyjrzyjmy się jednak szczegółom.   Menu i pasek ...
categories: windows oprogramowanie programowanie
---



IDE od Microsoftu pozwala na rozszerzenie możliwości środowiska programistycznego za pomocą wtyczek. Do jakich elementów Visual Studio można tworzyć wtyczki? W skrócie można napisać, że niemalże każda część składowa IDE jest podatna na rozbudowanie. Przyjrzyjmy się jednak szczegółom.   



### Menu i pasek narzędzi


IDE oferuje dodanie własnego menu i paska narzędzi. Zatem nie tylko otrzymujemy możliwość dodania opcji uruchomienia naszej wtyczki, ale także w ten sposób dodamy skrót do nowej funkcjonalności. Visual Studio oferuje gotowy szablon, dzięki któremu w kilka kliknięć wygenerujemy własne menu.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322183239_0.png)





### Okienka narzędziowe


Nic nie stoi na przeszkodzie, aby dodać własne okienko narzędziowe, albo rozszerzyć już te istniejące. Przyda się wiedza związana z XAML lub WinFroms.  



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322183239_1.PNG)





### Projekty


Narzędzia do Visual Studio umożliwiają stworzenie własnego szablonu projektu. Sami zaprojektujemy sposób organizacji plików w projekcie i zbudujemy startową solucję.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322183239_2.PNG)





### Opcje i ustawienia użytkownika


Tworząc własną wtyczkę musimy czasem dać użytkownikowi możliwość konfiguracji pluginu. SDK do Visual Studio oferuje możliwość dodania opcji do głównego okienka z ustawieniami IDE. Dodatkowo rozszerzymy ilość zapisywanych danych w momencie importu/eksportu preferencji użytkownika (Tools-&gt;Import/Export Settings).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322183239_3.png)





### Okienko właściwości


Nasz plugin może również poszerzyć okienko właściwości o nowe elementy, a także rozbudować już istniejące.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322183239_4.PNG)









### Najdrobniejsze elementy edytora Visual Studio


Programiści najczęściej obcują z edytorem i to właśnie on może zostać zmieniony przez wtyczki w najdrobniejszych szczegółach. Został oparty on na MEF, czym jest Managed Extensibility Framework pisałem we wcześniejszym [wpisie](https://www.dobreprogramy.pl/djfoxer/Managed-Extensibility-Framework-system-pluginow-do-aplikacji-.NET-od-Microsoftu,80021.html). Niemalże każdy element może zostać zmodyfikowany lub rozszerzony. Tutaj jednak warto zaznaczyć, że edytor posiada własne API oparte właśnie na MEF. Można powiedzieć, że zbudowany został na pojedynczych elementach MEF, które każdy programista może rozszerzyć.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322190613_0.png)



Obecnie edytor może być rozszerzony w następujących elementach:


  * mapowanie składni i analiza tekstu


  * formatowanie składni


  * paski przewijania i marginesy


  * tagi (tooltipy)


  * dekoracje (adornments) - własne obiekty (WPF) nakładane na edytor


  * obsługa eventów myszki


  * obsługa drag&amp;drop


  * własne opcje w edytorze


  * własne IntelliSense






### Inne elementy UI


Deweloperzy mogą także dynamiczne zarządzać solucją i projektami (listowanie, otwieranie, zamykanie, dodawanie, usuwanie, kompilacja) czy okienkami z outputem czy buildem. Rozszerzymy również okienko toolboxu, a także będzie nam dane pełne sterowanie paskiem statusu. Oczywiście to nie koniec, gdyż finalnie możemy stworzyć całkowicie samemu...





### Własne IDE


SDK pozwala również na to, aby budować własne IDE. Nic nie stoi na przeszkodzie, aby stworzyć nowe środowisko deweloperskie bazując na Visual Studio (Visual Studio Isolated Shell). Jest to świetna opcja do wydania specjalistycznego edytora dla konkretnej grupy programistów z własnym brandingiem i ficzerami.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-24-_16_/g_-_608x405_-_-_80061x20170322184602_0.png)


