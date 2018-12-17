---
layout:     post
title:      Ad Mediator, czyli dodajemy wiele sieci reklamowych do aplikacji Windows Phone
date:       2015-01-07 20:53:00
summary:    Sposobów na zarabianie na aplikacjach mobilnych jest bardzo dużo. Od udostępniania płatnych wersji oprogramowania, poprzez mikropłatności, aż do reklam umieszczanych wewnątrz aplikacji. Ten ostatni element nie wymaga dużego wkładu własnego od programisty, nie zmusza użytkowników do wydawania ciężko zarobionych pieniędzy, a dodatkowo jest możliwy do wdrożenia niemalże w każdym typie aplikacji. Co w...
categories: porady programowanie urządzenia mobilne
slug: Ad-Mediator-czyli-dodajemy-wiele-sieci-reklamowych-do-aplikacji-Windows-Phone,60151.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150106224628_0.png
---



Sposobów na zarabianie na aplikacjach mobilnych jest bardzo dużo. Od udostępniania płatnych wersji oprogramowania, poprzez mikropłatności, aż do reklam umieszczanych wewnątrz aplikacji. Ten ostatni element nie wymaga dużego wkładu własnego od programisty, nie zmusza użytkowników do wydawania ciężko zarobionych pieniędzy, a dodatkowo jest możliwy do wdrożenia niemalże w każdym typie aplikacji. Co więcej, reklama może być motorem napędowym do innych płatności. Wystarczy, że umieścimy wersję płatną bez reklam lub dodamy mikropłatność, która wyłączy reklamy.

Osoby tworzące aplikacje na Windows Phone w czystym środowisku deweloperskim mają gotową kontrolkę [AdControl](http://msdn.microsoft.com/en-us/library/advertising-mobile-windows-phone-adcontrol-class(v=msads.20).aspx),  która umożliwia proste wyświetlanie reklam Microsoft Advertising. Działa to wyśmienicie, ale jeśli chcielibyśmy dodać inne sieci reklamowe (w celu zwiększenia przychodów poprzez optymalizację reklamodawców do rynku) jak AdMob od Google czy AdDuplex, wówczas mamy nie lada problem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150106224628_0.png)




AdMob (Google), AdDuplex, Smaato i inne, mają własne SDK do obsługi reklam w Windows Phone. Aby móc wyświetlać reklamy od kilku reklamodawców należy zagłębić się w szczegóły konfiguracji każdej z kontrolek, a poza tym napisać kod, który będzie zarządzał kilkoma kontrolkami. Na pewno nie jest to ani proste, ani wydajne, a co więcej, możemy być pewnie, iż już ktoś miał identyczny problem i zapewne go dawno rozwiązał! 



Wszyscy znają zasadę DRY (Don’t Repeat Yourself), która zalecająca unikanie różnego rodzaju powtórzeń wykonywanych przez deweloperów. W obecnych czasach, gdzie mamy dostęp do sieci, forów i NuGeta, warto dodać jeszcze zasadę DROP: Don't Repeat Other People. Nie inaczej jest w tym przypadku. Od dłuższego czasu dostępna jest kontrolka [AdRotator](http://getadrotator.com/),  która współpracuje z wieloma sieciami reklamowymi i posiada ciekawy zestaw opcji. Jednakże warto wiedzieć, że w listopadzie 2014 Microsoft stworzył własną kontrolkę [Ad Mediator](https://visualstudiogallery.msdn.microsoft.com/401703a0-263e-4949-8f0f-738305d6ef4b)  do zarządzania wieloma sieciami reklamowymi pod Windows Phone. Jest to ciekawa alternatywa do AdRotator, a do tego posiada interesujące funkcje, które znacznie ułatwiają wdrożenie i konfigurację wielu sieci reklamowych. Olbrzymim plusem jest także możliwość zdalnego zarządzania kontrolką z poziomu [Dev Center](https://dev.windowsphone.com/en-us/dashboard). 


Ad Mediator wspiera Windows Phone 8.0/8.1 pod Silverlightem oraz Windows Phone 8.1 XAML. W przyszłości lista ta zostanie rozszerzona o aplikacje Windows Phone 8.1 tworzone w JavaScripcie oraz aplikacje pod Windows Store (Modern). Kontrolka posiada następujące sieci reklamowe (z uwzględnieniem wsparcia dla poszczególnych typów aplikacji):



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150106224618_0.png)



Implementacja i konfiguracja Ad Mediatora w Windows Phone nie jest skomplikowana. Oto poradnik jak krok pro kroku dodać wiele sieci reklamowych do własnej aplikacji na system mobilny od Microsoftu. 




### Dodanie Ad Mediatora do projektu



Pierwszą czynnością będzie pobranie rozszerzenia [Ad Mediator](https://visualstudiogallery.msdn.microsoft.com/401703a0-263e-4949-8f0f-738305d6ef4b)  i zainstalowanie go. Wówczas możemy przystąpić do dodania i konfiguracji kontrolki w projekcie:




  * Dodanie kontrolki do strony

Najszybszym sposobem stworzenia kontrolki jest przeciągnięcie AdMediatorControl z Toolboxa na okno Designera wybranej strony. Pamiętać należy, że każda kontrolka musi mieć własny, unikatowy ID w obrębie aplikacji:



```xml
  <WindowsPhone8:AdMediatorControl 
            x:Name="AdMediator_121F5B"
            Id="AdMediator-Id-ED7FED89-9736-4889-A807-894C9765148F" 
            Height="80"
            Width="480"
            VerticalAlignment="Top" 
            HorizontalAlignment="Center" />
```




  * Obsługa zdarzeń

W celu debugowania, jak i reakcji na zdarzenia (np. ukrywanie kontrolki, gdy nie ma reklam lub w przypadku braku dostępu do sieci), warto dodać eventy do AdMediatorControl:



```csharp


//problem z konfiguracją SDK wybranej sieci
void AdMediator_AdSdkEvent(object sender, AdSdkEventArgs e)
{
    Debug.WriteLine("AdSdk event {0} by {1}", e.EventName, e.Name);
}

//nie wyświetlą się żadne reklamy
void AdMediator_AdMediatorError(object sender, AdMediatorFailedEventArgs e)
{
    Debug.WriteLine("AdMediatorError:" + e.Error + " " + e.ErrorCode );
}

//kontrolka wyświetli reklamę z wybranej sieci
void AdMediator_AdFilled(object sender, AdSdkEventArgs e)
{
    Debug.WriteLine("AdFilled:" + e.Name);
}

//błąd wybranej sieci (brak połączenia z serwerem, brak reklam z sieci, itp.)
void AdMediator_AdError(object sender, AdFailedEventArgs e)
{
    Debug.WriteLine("AdSdkError by {0} ErrorCode: {1} ErrorDescription: {2} 
                Error: {3}",e.Name, e.ErrorCode, e.ErrorDescription, e.Error);
}
```





  * Obsługa nieoczekiwanych wyjątków ze strony poszczególnych sieci reklamowych


Zaleca się, aby do pliku App.xaml.cs dodać obsługę wyjątków sieci reklamowych. Dzięki temu będziemy w stanie uniknąć  *wywrócenia*  się aplikacji spowodowanej błędem, którejś z wtyczek zewnętrznych. W zdarzeniu UnhandledException dodajemy:



```csharp


    if (e != null)
   {
       Exception exception = e.ExceptionObject;
       if ((exception is XmlException || exception is NullReferenceException) && exception.ToString().ToUpper().Contains("INNERACTIVE"))
       {
           Debug.WriteLine("Handled Inneractive exception {0}", exception);
           e.Handled = true;
           return;
       }
       else if (exception is NullReferenceException && exception.ToString().ToUpper().Contains("SOMA"))
       {
           Debug.WriteLine("Handled Smaato null reference exception {0}", exception);
           e.Handled = true;
           return;
       }
       else if ((exception is System.IO.IOException || exception is NullReferenceException) && exception.ToString().ToUpper().Contains("GOOGLE"))
      {
          Debug.WriteLine("Handled Google exception {0}", exception);
          e.Handled = true;
          return;
       }
       else if (exception is ObjectDisposedException && exception.ToString().ToUpper().Contains("MOBFOX"))
       {
           Debug.WriteLine("Handled Mobfox exception {0}", exception);
           e.Handled = true;
           return;
       }
       else if ((exception is NullReferenceException || exception is XamlParseException) && exception.ToString().ToUpper().Contains("MICROSOFT.ADVERTISING"))
       {
           Debug.WriteLine("Handled Microsoft.Advertising exception {0}", exception);
           e.Handled = true;
           return;
       }
              
   }



```











### Konfiguracja poszczególnych reklamodawców w Visual Studio



Przyszedł czas na konfiguracje sieci reklamowych. W przykładzie użyję Microsoft Advertising, AdDuplex oraz AdMob (Google).




  * Dodanie sieci reklamowych

Ad Mediator umożliwia szybkie dodanie wybranych sieci reklamowych. W tym celu należy na projekcie Windows Phone kliknąć prawym przyciskiem i wybrać opcję:

Add->ConnectedService...



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150106234219_0.png)



a w nowo otwartym oknie  *Services Manager*  wybrać

 * Select ad networks* 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150106235000_0.png)



Zaznaczamy w tym miejscu sieci reklamowe, jakie mają być dostępne w aplikacji.





  * Ręczne dodanie brakujących bibliotek



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150106235009_0.png)



W przykładzie zarówno Microsoft Advertising, jak i AdDuplex nie wymagają dodatkowych bibliotek do działania (inaczej mówiąc Ad Mediator pobierze je za nas). Inaczej jest jednak z AdMob. W tym przypadku aplikacja nie może pobrać dllek i musimy dodać je ręcznie, pobierając paczkę ok. 250 KB ze strony [ Google Mobile Ads SDK](https://developers.google.com/mobile-ads-sdk/download#download)  


  * Dane dostępowe



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107000050_0.png)



Jeśli wszystko udało się poprawnie dołączyć do projektu, każda z sieci będzie posiadała status  *Fetched*  w oknie  *Services Manager*  (jeśli mimo wszystko jest inaczej, patrz niżej). Teraz przyszedł czas na szybką konfiguracje sieci, poprzez identyfikatory, które wygenerowaliśmy/dostaliśmy od poszczególnych reklamodawców:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107000100_0.png)


 



  * Konfiguracja funkcji

Jak zapewne zauważyliście, każda z sieci posiada listę funkcji, które musi spełniać aplikacja, aby móc taką sieć reklamową dodać. Są to niezbędne elementy, które wykorzystywane są przez kontrolkę jak np. możliwość dostępu do sieci, czy wykorzystanie kontrolki webowej.

W tym celu w oknie  *Services Manager*  należy przejrzeć ostatnia kolumnę * Required capabilities*  i w pliku WMAppManifest.xml dodać wymagana opcje:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107000050_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107000951_0.png)







Tak skonfigurowana aplikacja powinna już wyświetlać reklamy:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107195116_0.png)






### Zdalna konfiguracja reklamodawców przez DevCenter



Jedną z najbardziej wartościowych funkcji Ad Mediatora jest pełna integracja z centrum deweloperskim DevCenter. Po dodaniu aplikacji poprzez portal, DevCenter sam wykryje obecność Ad Mediatora i aktywuje panel do zdalnej konfiguracji kontrolki.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107200011_0.png)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2015-1-7-_77_/g_-_-x-_-_-_x20150107200019_0.png)




W ty miejscu można skonfigurować:



  * czy dana konfiguracja będzie obejmowała wszystkie markety, czy zostanie dostosowana do konkretnego marketu (języka) 

  * rozdzielenie procentowe reklamodawców:



  * automatyczny, równomierny podział

  * ręczne ustalenie procentowe



W tym miejscu można również ustalić czy sieć reklamowa ma być całkowicie wyłączona lub pełnić rolę zapasową



  * dane dostępowe od poszczególnych sieci reklamowych

  * rozmiar bannerów

  * czas odświeżenia




Plik konfiguracyjny Ad Mediatora można pobrać klikając na  *Download config* , w celu podmiany domyślnie stworzonego pliku w Visual Studio, aby ten nie nadpisywał konfiguracji w DevCenter podczas wgrywania nowej wersji.



### Najczęstsze problemy i ich rozwiązania


Mimo, że Ad Mediator jest niesłychanie prostym i przyjemnym narzędziem, zdarzają się często małe, ale uciążliwe problemy. Oto kilka z nich, wraz ze wskazówkami na ich rozwiązanie:




  * Żadna z reklam się nie wyświetla

Najszybszą analizą takiego problemu jest podczepienie zdarzenia  *AdError* , opisanego w punkcie  *Obsługa zdarzeń* . W tym miejscu kontrolka zwraca szczegółowe dane odnośnie jaka sieć reklamowa zwróciła wyjątek, z opisem i kodem błędu.


  * Brak reklam na emulatorze

Jest to całkiem normalna przypadłość. Polecam przetestowanie reklam poprzez wgranie aplikacji na realne urządzenie.

  * Ad Mediator nie widzi dllek sieci reklamowych wgranych ręcznie (AdMob i inne) [status Not Fetched]

Jeśli Ad Mediator pokazuje stan dllki na Not Fetched lub Dev Center wskazuje brak dllki w projekcie, pomimo dodania jej do projektu, wówczas warto usunąć sieć reklamową z Ad Mediatora. Należy jednak zrobić to z poziomu NuGeta. W oknie menadżera pakietów usuwamy problematyczną sieć. W tym momencie upewniamy się, że potrzebne dllki są już w projekcie i ponownie dodajemy sieć reklamową poprzez Ad Mediatora, który sam doda niezbędne pakiety z NuGeta.
 

  * Jak dostosować sieci reklamowe i ich procentowy udział?

Jest to najtrudniejsze z zadań podczas dodawania reklam. W wielu przypadkach różne sieci reklamowe posiadają więcej lub mniej reklam w zależności od regionu. Dodatkowo niektóre sieci nie zawsze mają w danym momencie przygotowaną reklamę w danym regionie i kategorii (występuje to często w przypadku naszego regionu w Microsoft Advertising). Warto również zainteresować się AdDuplexem, który pomaga deweloperem we wzajemnej reklamie ich aplikacji.




Mam nadzieję, że ten poradnik będzie pomocny przy tworzeniu aplikacji i zarabianiu na nich. Życzę wszystkim wysokiego współczynnika klikalności (CTR) :D



