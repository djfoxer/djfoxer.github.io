---
layout:     post
title:      Zaczynamy zabawę z rozszerzeniami do Visual Studio 
date:       2017-03-15 21:49:00
summary:    Jeszcze kilka lat temu pisanie rozszerzeń do IDE od Microsoftu było nie lada wyzwaniem. Szczątkowa dokumentacja, skomplikowane API utrudniały tylko pracę deweloperom chcącym stworzyć własne rozszerzenie.Obecnie sytuacja jest znacznie prostsza, Microsoft udostępnia wiele przykładów i rozwiązań, które pomogą początkującym programistom w temacie wtyczek do Visual Studio.  W tym wpisie przedstawię kil...
categories: windows porady programowanie
slug: Zaczynamy-zabawe-z-rozszerzeniami-do-Visual-Studio,79883.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315214228_0.png
---



Jeszcze kilka lat temu pisanie rozszerzeń do IDE od Microsoftu było nie lada wyzwaniem. Szczątkowa dokumentacja, skomplikowane API utrudniały tylko pracę deweloperom chcącym stworzyć własne rozszerzenie.

Obecnie sytuacja jest znacznie prostsza, Microsoft udostępnia wiele przykładów i rozwiązań, które pomogą początkującym programistom w temacie wtyczek do Visual Studio.  W tym wpisie przedstawię kilka porad jak szybko zacząć tworzyć dodatki i z czego warto korzystać.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315214228_0.png)





## Visual Studio SDK


Do rozpoczęcia pracy wymagane jest zainstalowanie Visual Studio SDK. Obecnie w nowej wersji 2017 zrobimy to zaznaczając odpowiednią opcję.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315211847_0.PNG)



Na co pozwala SDK? Niemalże na wszystko. Poszczególne główne elementy składowe Visual Studio są właśnie takimi wbudowanym rozszerzeniami. Deweloperzy dostają od Microsoftu biblioteki, które używane są przy tworzeniu IDE. Dzięki czemu zbudujemy zatem pojedyncze menu, będziemy mogli kontrolować pasek stanu, rozszerzymy możliwości edytora czy zaprojektujemy dokowane okno, ale również stworzymy wsparcie dla nowego języka programowania. To wszystko bez dodatkowych narzędzi czy oddzielnych IDE.



## Visual Studio Experimental Instance


W celu debugowania i tworzonych rozszerzeń, Microsoft przedstawił ciekawą opcję "klonowania" Visual Studio. Visual Studio Experimental Instance jest oddzielną instancją IDE, która odpala się przy debugowaniu wtyczek.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315211853_0.PNG)



Jest to Visual Studio, które ma oddzielne zapisy w rejestrze, przez co możemy spokojnie "psuć" takie IDE, w celu testowania tworzonych dodatków.



## Extensibility Tools


Rozpoczynając przygodę z wtyczkami do Visual Studio warto wyposażyć się w rozszerzenie [Extensibility Tools](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ExtensibilityTools).  Dodatek ten oferuje olbrzymią ilość małych ficzerów, które ułatwią znacznie pracę z pluginami do IDE.




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315211854_0.png)



Projekt jest rekomendowany przez Microsoft, jako narzędzie * Must Have*  przy wchodzeniu w temat dodatków do Visual Studio. Grzech będzie zatem nie zainstlowanie go :)



## Wiedza w sieci


Temat wymaga na początku zgłębienia podstawowych rzeczy, które nie są tak bardzo oczywiste. W sieci jest całkiem sporo stron, które oferują taką wiedzę. Sam jeszcze raczkuję, jeśli chodzi o pluginy do VS, ale mogę polecić kila stron, które mogą znacznie pomóc w dewelopingu.

Króciutkie wprowadzenie zapewnił sam Microsoft na podstronie [Extensions for Visual Studio](https://www.visualstudio.com/en-us/docs/integrate/ide/extensions/overview),  zaś pełna dokumentacja dostępna jest tutaj: [Visual Studio Extensibility Documentation](https://docs.microsoft.com/pl-pl/visualstudio/extensibility/index).  Mamy tam wiele przykładów i gotowych rozwiązań. Lektura obowiązkowa.

Najciekawsze jest jednak to, że Microsoft udostępnia kilkadziesiąt gotowych przykładowych rozszerzeń. Z pełnym opisem i kodem źródłowym, gotowym do pobrania i odpalenia w Visual Studio. Wszystko dostępne jest na [Githubie](https://github.com/Microsoft/VSSDK-Extensibility-Samples). 

Dodatkowo dostępny jest otwarty chat na [Gitterze](https://gitter.im/Microsoft/extendvs),  gdzie zawsze ktoś się znajdzie, kto udzieli odpowiedzi na nurtujące pytanie w temacie wtyczek do IDE.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315214228_1.PNG)





## A może jakaś książka?


Wybór nie jest duży. Z płatnych pozycji można polecić dwie książki:




  * Professional Visual Studio Extensibility - Keyvan Nayyeri

  * Microsoft Visual Studio 2015 Unleashed - Lars Powers, Mike Snell



Można również pobrać całkowicie za darmo książkę Visual Studio Add-Ins Succinctly (Joe Booth), dostępną na stronie [Syncfusion](https://www.syncfusion.com/resources/techportal/details/ebooks/visualstudio).  



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2017-3-15-_33_/g_-_-x-_-_-_x20170315214228_2.PNG)





### Co dalej...


W kolejnym wpisie będzie przykładowa wtyczka  *Hello World*  z kilkoma prostymi elementami, jakie można dodać do IDE. Możliwości jakie daje Visual Studio SDK są olbrzymie, jest o czym czytać :)