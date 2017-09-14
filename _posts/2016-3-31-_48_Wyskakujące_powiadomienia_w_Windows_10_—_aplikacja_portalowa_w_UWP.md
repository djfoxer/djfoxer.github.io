---
layout:     post
title:      Wyskakujące powiadomienia w Windows 10 — aplikacja portalowa w UWP
date:       2016-03-31 22:47:00
summary:    Ostatnio pokazałem  pierwszą działającą wersję aplikacji w UWP (Universal Windows Platform), która posiadała logowanie i wyświetlała prosty, niesformatowany tekst powiadomień. W dzisiejszym wpisie przedstawię kolejne nowe rzeczy, jakie dodałem do programu.Toast notifications w Windows 10Microsoft w nowej wersji okienek udostępnił znacznie poprawiony system powiadomień. Opiera się on na dokumencie ...
categories: windows programowanie urządzenia mobilne
---



Ostatnio pokazałem  pierwszą działającą wersję aplikacji w UWP (Universal Windows Platform), która posiadała logowanie i wyświetlała prosty, niesformatowany tekst powiadomień. W dzisiejszym wpisie przedstawię kolejne nowe rzeczy, jakie dodałem do programu.



## Toast notifications w Windows 10

Microsoft w nowej wersji okienek udostępnił znacznie poprawiony system powiadomień. Opiera się on na dokumencie XML i umożliwia całkiem sporą konfigurację. Oczywiście notyfikacje dostępne są zarówno na Windows 10, jak i na mobilnych okienkach. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222300_1.png)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222300_2.png)


W tej wersji dostaliśmy większe pole do popisu, jeśli chodzi o dostosowanie powiadomienia do własnych potrzeb. Możemy dodawać przyciski, zmieniać ułożenie tekstu czy grafiki, a także umieścić pole tekstowe (idealne do szybkich odpowiedzi na SMSa). Powiadomienia trafiają również do Centrum Akcji i mogą posiadać własny schemat dźwiękowy.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222300_3.png)


Zobaczmy zatem jak wygląda to w praktyce, na przykładzie tworzonej aplikacji.


## Wyskakujące powiadomienia z dobreprogramy.pl


Zacznijmy zatem od szablonu XML, jaki będzie użyty w naszym przypadku. Na tę chwilę jest on jawne wklejony jako string. Do operacji na XML używać będę klasy  *XmlDocument* :


```csharp

XmlDocument toastXml = new XmlDocument();
toastXml.LoadXml(
    $@"
<toast>
    <visual>
        <binding template='ToastGeneric'>
            <text></text>
            <text></text>
            <text></text>
            <image placement='appLogoOverride'></image>
        </binding>
    </visual>
    <actions>
        <action
            content='pokaż'
            activationType='foreground'
            arguments='show'/>

        <action
            content='anuluj'
            activationType='foreground'
            arguments='hide'/>
    </actions>
</toast>"
);

```



Oczywiście można nie bawić się i użyć, któregoś z dostępnych [szablonów](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.notifications.toasttemplatetype). Przykładowy schemat z grafiką i 3 linijkami tekstu ( *ToastImageAndText04* ) ładujemy w następujący sposób:


```csharp

toastXml = 
ToastNotificationManager.GetTemplateContent(ToastTemplateType.ToastImageAndText04);

```


Nasz szablon składa się z trzech pól tekstowych (pierwsze będzie pogrubione) i grafiki. Obrazek posiada atrybut   *placement='appLogoOverride'* , określa on w tym przypadku, iż będziemy nadpisywali ikonę w powiadomieniu (domyślną ikonę aplikacji) własną grafiką. Dwa przyciski action:  *pokaż*  i  *anuluj*  będą odpowiednio otwierały stronę www do przypisanego powiadomienia lub zamykały notyfikację (ewentualnie oznaczały powiadomienia jako przeczytane). Atrybut  *activationType*  z  *foreground*  określa, że akcje będą działały na uruchomionej aplikacji w głównym planie. Atrybuty  *arguments*  w przyciskach pozwolą na rozróżnienie w jaki element kliknęliśmy.

Mając zatem zmienną  *notification* , która jest pojedynczym powiadomieniem, powyższy szablon uzupełniamy w następujący sposób:


```csharp

XmlNodeList toastImageAttributes = toastXml.GetElementsByTagName("image");
((XmlElement)toastImageAttributes[0]).SetAttribute("src", notification.Avatar);
((XmlElement)toastImageAttributes[0]).SetAttribute("alt", "img");

XmlNodeList toastTextAttributes = toastXml.GetElementsByTagName("text");
toastTextAttributes[0].InnerText = notification.Title;
toastTextAttributes[1].InnerText = notification.AddedDate.
                    ToString("dd.MM.yyyy HH:mm:ss", CultureInfo.InvariantCulture);
toastTextAttributes[2].InnerText = notification.FullText;

toastTextAttributes = toastXml.GetElementsByTagName("actions");
((XmlElement)toastTextAttributes[0]).SetAttribute("url", notification.TargetUrl);

```


Dodatkowo dodaję atrybut  *url* , który posiada adres www, związany z powiadomieniem.

Podczepienie zdarzenia na kliknięcie w przycisk jest tworzone poprzez event  *Activated* :


```csharp

ToastNotification toast = new ToastNotification(toastXml);
toast.Activated += Toast_Activated;


```


obsługa eventu:


```csharp

private async void Toast_Activated(ToastNotification sender, object args)
{
    if ((args as ToastActivatedEventArgs).Arguments == "show")
    {
       string url=((XmlElement)sender.Content.GetElementsByTagName("actions").First())
                    .GetAttribute("url");
       if (!string.IsNullOrEmpty(url))
       {
            await Launcher.LaunchUriAsync(new Uri(url));
       }
    }
}

```


W przypadku kliknięcia przycisku  *pokaż*  ( *arguments=show* ), pobieramy url powiadomienia i otwieramy domyślną przeglądarkę.

Notyfikacja pokazuje się po wywołaniu funkcji  *Show* :


```csharp

ToastNotificationManager.CreateToastNotifier().Show(toast);

```



## Powiadomienia w akcji


Jak zatem wyglądają notyfikacje "na żywo"? Sprawdźmy:


### Windows 10



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222312_2.PNG)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331223202_0.png)



### Windows 10 Mobile




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331223006_0.png)


Myślę, że prezentuje się to już całkiem  *zacnie*  i od strony UI jestem całkiem zadowolony. Kod C# jeszcze zapewne będzie się zmieniał. Kliknięcie na przycisk przenosi już do odpowiedniej strony www.

Jeszcze na koniec dwa screeny z delikatnie odświeżonej listy z powiadomieniami w aplikacji (pierwszy screen to aplikacja na Windows 10, drugi pochodzi z wersji mobilnej):


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222312_4.png)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222312_1.PNG)



## Kolejny wpis

Następne posty będą związane już z działaniem aplikacji w tle i pobieraniem/uzyskiwaniem powiadomień przy wyłączonym programie. Temat już wstępnie przejrzałem i będzie ciężko. Domyślnie aplikacje UWP mogą uruchamiać wątek minimalnie co 15 minut (!!??) lub odbierać powiadomienia "na żywo", ale wymaga to wykupienia miejsca na Azure. Na pewno kolejne odsłona serii będzie ciekawa :) Zachęcam do substytucji ;) 

Sam wpis może pojawić się trochę później, gdyż w ten weekend jadę do Dębna na maraton :) Trzymajcie kciuki ;)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331223741_0.png)


Do kolejnego :)



> Aktualne źródła można znaleźć na GitHub pod adresem:
> [https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-3-31-_48_/g_-_608x405_-_-_71904x20160331222300_0.png)
