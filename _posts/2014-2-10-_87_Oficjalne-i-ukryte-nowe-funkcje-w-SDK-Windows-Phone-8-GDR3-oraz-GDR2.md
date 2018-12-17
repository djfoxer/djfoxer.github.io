---
layout:     post
title:      Oficjalne i ukryte nowe funkcje w SDK Windows Phone 8 GDR3 (oraz GDR2)
date:       2014-02-10 17:32:00
summary:    Wraz z premierą Windows Phone 8 GDR3 Microsoft dodał kilka nowych elementów do SDK. Nie są to jakiejś rewolucyjne zmiany, ale interesujące funkcjonalności, które mogą się przydać przy tworzeniu aplikacji na nowy system mobilny z Redmond. Najciekawsze jednak jest to, że część rzeczy nie jest dostępna bezpośrednio, a do niektórych elementów nie znajdziemy nawet wzmianki w MSDNie.Jaką masz wersję opr...
categories: porady programowanie urządzenia mobilne
slug: Oficjalne-i-ukryte-nowe-funkcje-w-SDK-Windows-Phone-8-GDR3-oraz-GDR2,51929.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-2-10-_87_/g_-_-x-_-_-_x20140208221727_0.png
---



Wraz z premierą Windows Phone 8 GDR3 Microsoft dodał kilka nowych elementów do SDK. Nie są to jakiejś rewolucyjne zmiany, ale interesujące funkcjonalności, które mogą się przydać przy tworzeniu aplikacji na nowy system mobilny z Redmond. Najciekawsze jednak jest to, że część rzeczy nie jest dostępna bezpośrednio, a do niektórych elementów nie znajdziemy nawet wzmianki w MSDNie.



## Jaką masz wersję oprogramowania?


Najważniejszym elementem w dobieraniu się do tego typu  *ukrytych*  funkcjonalności jest sprawdzenie na jakiej wersji systemu działa kod. Można to zrobić w bardzo prosty sposób:



```csharp

private static Version GDR3 = new Version(8, 0, 10492);
private static Version GDR2 = new Version(8, 0, 10322);

public static bool HasGDR2
{
    get { return Environment.OSVersion.Version >= GDR2; }
}

public static bool HasGDR3
{
    get { return Environment.OSVersion.Version >= GDR3; }
}


```


 
Takie sprawdzenie będzie niezbędne, aby nie wyłożyć naszego kodu, gdyż wcześniejsze wersje systemu nie posiadają omawianych funkcji.

Zatem przejdźmy do nowości.



## Blokada robienia zrzutu ekranu przez użytkownika


Microsoft w GDR2 wprowadził możliwość blokowania robienia zrzutów ekranu. Nieodblokowany system Windows Phone 7.x nie miał możliwości robienia screenów. Od wersji 8 możemy zrobić zrzuty ekrany za pomocą kombinacji klawiszy: [Power]+[Windows]. Najwidoczniej taka opcja nie jest zawsze pożądana, stąd też od wersji GDR2 (odkryto to dopiero przy wersji GDR3) można z poziomu aplikacji dynamicznie zablokować robienie zrzutów ekranu.

Nieudokumentowana przez Microsoft właściwość  *IScreenCaptureEnabled*  w klasie  *PhoneApplicationPage*  pozwala na blokowanie i odblokowanie robienia screenów podczas działania aplikacji. Aby dostać się do właściwości trzeba posłużyć się mechanizmem refleksji. Poniższy kod działa jako extension method do instancji klasy  *PhoneApplicationPage*  ("strona" w Windows Phone dziedziczy po tej klasie):



```csharp

public static bool SetScreenCaptureEnabled(this PhoneApplicationPage page, bool enable)
{
    if (HasGDR2)
        page.GetType().GetProperty("IsScreenCaptureEnabled").SetValue(page, enable);
        return true;
    else
        return false;
}

public static bool? IsScreenCaptureEnabled(this PhoneApplicationPage page)
{
    if (HasGDR2)
       return (bool)page.GetType().GetProperty("IsScreenCaptureEnabled").GetValue(page);
    else
        return null;
}


```



Metoda  *SetScreenCaptureEnabled(enable)*  pozwoli na ustawienia właściwości ( *true/false* ), a  *IsScreenCaptureEnabled()*  sprawdzimy aktualny stan. 

Zablokowanie spowoduje niemożność zrobienia zrzutu ekranu. Przy próbie zrobienia screenshota pojawi się komunikat (tutaj w j. polskim) zarówno w aplikacji, jak i w menadżerze procesów: 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-2-10-_87_/g_-_-x-_-_-_x20140208221727_0.png)





## Powiadomienia Toast z możliwością ustawienia własnych dźwięków


Kolejną nowością, której nie znajdziemy bezpośrednio jest ustawienie dźwięku powiadomień. Od wersji GDR3 każde wyskakujące powiadomienie może mieć przyporządkowany własny dźwięk ustawiany z poziomu kodu. Tutaj również należy użyć mechanizmu refleksji. Metoda rozszerzająca dla  *ShellToast*  wygląda następująco:



```csharp

public static void SetSound(this ShellToast shellToast, Uri uri)
{
    if (HasGDR3)
        shellToast.GetType().GetProperty("Sound").SetValue(shellToast, uri);
}

```



Teraz Tworząc  *ShellToast*  wystarczy odpowiednio wywołać metodę.:


```csharp

ShellToast toast = new ShellToast();
toast.Title = "Toast Sound";
toast.Content = "My custom sound";
toast.SetSound(new Uri("/Assets/horn.mp3", UriKind.Relative));
toast.Show();

```



wówczas nasze powiadomienie będzie miało unikalny dźwięk.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-2-10-_87_/g_-_-x-_-_-_x20140208223529_0.png)



Przy okazji dodam, że od wersji GDR3 powiadomienia Toast mogą "wyskakiwać" także gdy dana aplikacja jest na pierwszym planie, ale została przysłonięta przez rozmowę lub wygaszacz.



## Sprawdzenie czy powiadomienia zostaną wyświetlone ze względu na oszczędzanie energii



Małym elementem w GDR3, który może być przydatny jest sprawdzenie czy powiadomienie zostanie wyświetlone ze względu na oszczędzanie energii. Kiedy użytkownik aktywuje tryb energooszczędny, wówczas powiadomienia nie zostaną uruchomione. Jeśli zajdzie taka potrzeba można to sprawdzić i poinformować o tym użytkownika. Właściwość "ukryta" jest w statycznej klasie  *PowerManager* , do której dostaniemy się oczywiście przez refleksję:



```csharp

public bool? IsPowerSavingModeEnabled()
{
    if (HasGDR3)
        return (bool)typeof(PowerManager).GetProperty("PowerSavingModeEnabled").GetValue(null);
    else
        return null;
}

```





## Pozostałe zmiany w GDR3


Prócz powyższych zmian, mamy jeszcze kilka pomniejszych jak:



  * Nowe skróty do ustawień systemu:




  * oszczędzanie baterii:


```csharp

Windows.System.Launcher.LaunchUriAsync(new Uri("ms-settings-power:"));

```



  * rotacja ekranu:


```csharp

Windows.System.Launcher.LaunchUriAsync(new Uri("ms-settings-screenrotation:"));

```






  * Aplikacje mogą maksymalnie zajmować 570 MB pamięci na urządzeniach z 2GB RAM

  * Pamięć dla plików audio w tle zwiększyła się do 25 MB

  * Zmieniono sposób obliczania właściwości  *device-width*  w mobilnym IE (160 * realna szerokość w calach lub przybliżona wartość)

  * nowa rozdzielczość 1080p





## Koniec :)


Wydaje się, że są to jedyne realne (i możliwe do użycia, gdyż dodano elementy nieodstępne dla zwykłych aplikacji, jak np. blokowanie połączeń/sms ) nowości jakie zostały umieszczone w GDR3 (i GDR2). Chyba, że ktoś jeszcze coś ciekawego znajdzie :)
