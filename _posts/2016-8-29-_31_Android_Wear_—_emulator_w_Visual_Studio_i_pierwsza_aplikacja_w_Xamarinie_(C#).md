---
layout:     post
title:      Android Wear — emulator w Visual Studio i pierwsza aplikacja w Xamarinie (C#)
date:       2016-08-29 18:41:00
summary:    Testy Motoroli Moto 360 2 w akcji Lenovo pokazały spory potencjał w aplikacjach na Android Wear. Zupełnym przypadkiem od jakiegoś już czasu grzebię się w Xamarinie, czyli platformie skierowanej do programistów .NET (C#) do tworzenia multiplatformowych aplikacji (nie tylko mobilnych). Z czystej cieka...
categories: windows programowanie urządzenia mobilne
---



Testy [Motoroli Moto 360 2](http://www.dobreprogramy.pl/djfoxer/Motorola-Moto-360-2-generacji-recenzja-na-sportowo,75871.html) w [akcji Lenovo](http://www.dobreprogramy.pl/Lenovo) pokazały spory potencjał w aplikacjach na Android Wear. Zupełnym przypadkiem od jakiegoś już czasu grzebię się w Xamarinie, czyli platformie skierowanej do programistów .NET (C#) do tworzenia multiplatformowych aplikacji (nie tylko mobilnych). Z czystej ciekawości postanowiłem sprawdzić, jak wygląda pisanie oprogramowania na Android Wear od strony dewelopera .NET. W pierwszej kolejności potrzebny będzie nam...



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827114405_0.jpg)





## Emulator


Prace nad przygotowaniem wpisu i aplikacji zacząłem jeszcze na fizycznym zegarku (więcej o testowanym [Moto 360 2](http://www.dobreprogramy.pl/djfoxer/Motorola-Moto-360-2-generacji-recenzja-na-sportowo,75871.html)), ale niestety czas szybko zleciał i trzeba było oddać smartwatch. Na szczęście z pomocą przychodzą emulatory.

Microsoft udostępnił świetny dodatek [Visual Studio Emulator for Android](https://beta.visualstudio.com/vs/msft-android-emulator/), który uruchamia dowolną wersję Androida na Windowsie. Dodatkowo całość oparta jest na Hyper-V, dzięki czemu emulator działać bardzo szybko, o kilka klas lepiej niż to co otrzymujemy w SDK od Googla na okienkach. Niestety...



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160826011907_0.png)



Visual Studio Emulator for Android nie doczekał się jeszcze obsługi Android Wear, przez co trzeba na daną chwilę korzystać z emulatora dostarczonego wraz z SDK Androida. Najgorsze jest to, że na Windowsie jest spora ilość problemów z jego uruchomieniem.



### Pobieranie plików

 
Zakładam, że już macie [zainstalowanego](https://msdn.microsoft.com/en-us/library/mt613162.aspx) Xamarina w Visual Studio.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827111525_0.jpg)



W takim wypadku przechodzimy do Android SDK Managera (w Visual Studio menu Tools - Android). Tutaj klikamy na Tools-Android SDK Tools i Android SDK Platform-tools. Dodatkowo w wybranej wersji Androida (co najmniej 4.4, najlepiej wybrać najnowszą, w moim przypadku to 7.0, aczkolwiek warto mieć także wersję 6.0, która skompiluje nam projekt w VS) zaznaczamy potrzebne pakiety, pamiętając o Android Wear.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160826011333_0.PNG)





### Konfiguracja emulatora


Przyszedł zatem czas na konfigurację emulatora Android Wear pod Visual Studio. Będąc już w IDE wybieramy z menu Tools - Android - Android Emulator Manager. Po uruchomieniu Android Virtual Device (AVD) Managera przechodzimy do zakładki Device Definitions.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827104014_0.PNG)



Wybieramy dowolne urządzenie z Android Wear. Ze względu na to, że przyzwyczaiłem się już do okrągłego ekranu Moto 360 zaznaczam: Android Wear Round. Teraz stworzymy nową &quot;maszynę wirtualną&quot; na podstawie definicji zaznaczanego urządzenia klikając na przycisk &quot;Create AVD...&quot;

W nowym oknie sprawdzamy, czy mamy żądaną wersję Androida i urządzenia (w tym przypadku Android 7.0 i Android Wear). Musimy także wybrać odpowiedni skin emulatora i wersję procesora pod Android Wear, o tym ostatnim za chwilę. Warto zaznaczyć także &quot;Use Host GPU&quot;, w moim przypadku brak tej opcji powodował nieprawidłowe wyświetlanie ekranu urządzenia  na emulatorze. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827104249_0.PNG)





### CPU: ARM vs Intel Atom - Windows 10 Anniversary Update suxx


Emulować możemy dwa typu procesorów. Podstawowy to ARM z którym zapewne nie będzie żadnych problemów (poza tym, że jest wolny).

Najciekawszą opcją jest jednak emulator oparty na Intel Atom, dzięki temu, iż wspiera wirtualizację sprzętową i działa do 10x szybciej niż emulator ARM. Jest z nim jednak kilka problemów. Jeśli mamy w systemie aktywowane Hyper-V, to musimy je dezaktywować (i uruchomić ponownie system), najszybciej z linii komend: 


```shell

bcdedit /set hypervisorlaunchtype off

```


Dodatkowo musimy mieć HAXM (Intel&#174; Hardware Accelerated Execution Manager). Silnik wirtualizacji pobieramy tutaj: [Intel&#174; HAXM](https://software.intel.com/en-us/android/articles/intel-hardware-accelerated-execution-manager). Wszsytko było by piękne gdyby nie to, że wersja HAXM w obecnej wersji (6.0.3) gryzie się z Windows 10 Anniversary Update! Na daną chwilę, osoby z najnowszą aktualizacją do Windows 10, nie są w stanie skorzystać z HAXM, a co za tym idzie uruchomić emulatora bazującego na Intel Atom. Niestety w takim przypadku zostaje tylko wybór wolniejszego emulatora ARM.



### Odpalamy emulator


Jeśli wszystko zrobiliśmy poprawnie, wówczas na pierwszej zakładce Android Virtual Device (AVD) Managera mamy stworzony emulator Android Wear:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827111146_0.PNG)



Wystarczy tylko kliknąć na &quot;Start&quot; i &quot;Launch&quot;, aby uruchomić nasz nowiutki emulator Android Wear:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827111950_0.PNG)



W tym momencie możemy pobawić się systemem. Tu mała uwaga, w tym momencie wybraliśmy emulator z najnowszą wersją systemu, czyli... Android Wear 2.0!



## Xamarin Android Wear w Visual Studio


Przyszedł czas na uruchomienie pierwszej aplikacji na naszym emulatorze Android Wear. Klikamy na File - New- Project i z okna wybieramy Wear App (Android). Możemy także w ramach testów i nauki pobrać jeden z dostępnych projektów na stronie [Xamarina](https://developer.xamarin.com/samples/android/Android%20Wear/).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827112548_0.PNG)



W projekcie wybierzmy także odpowiednią wersję Androida, która skompiluje nam projekt:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827120815_0.PNG)



Z górnej belki wybieramy stworzony emulator:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827113117_0.PNG)



i odpalamy nasz projekt


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827113333_0.PNG)



Pierwsze uruchomienie może trochę potrwać. IDE wrzuci na Android Wear prócz naszej aplikacji także niezbędne pakiety: Mono Shared Runtime i Xamarin.Android API Support, do prac deweloperskich. Po kilku chwilach naszym oczom ukarzę się pierwsza stworzona aplikacja na Android Wear:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-8-29-_31_/g_-_608x405_-_-_75962x20160827114128_0.PNG)





## Podsumowanie


Android Wear to dość świeża platforma, tym bardziej framework na Xamarina to niezmiernie nowa odnoga na tej platformie. Warto dodać, że aplikacje na Android Wear można pisać w C# tylko w czystym Xamarinie, nie użyjemy tutaj Xamarin.Forms. Postawienie emulatora może sprawić trochę problemów, ale uważam, że warto. Chętni powinni spróbować swoich sił z aplikacjami na Android Weara już teraz. Aplikacje na zegarek używają wielu tych samych kontrolek, co zwykłe aplikacja na Androida. W większości przypadków apki na Android Wear współpracować będę z tymi &quot;większymi&quot; na smartfonie. Do wymianach danych pomiędzy nimi służy Data API i Message API, ale to już temat na inny wpis...


