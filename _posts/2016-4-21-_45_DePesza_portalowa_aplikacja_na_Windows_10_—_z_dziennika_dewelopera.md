---
layout:     post
title:      DePesza portalowa aplikacja na Windows 10 — z dziennika dewelopera
date:       2016-04-21 17:14:00
summary:    Prace nad aplikacją nadal trwają. Dziękuję, za docenienie tej serii i oddane głosy na moje wpisy w marcowym konkursie blogowym ;)Jak już zapewne zauważaliście, została wybrana nazwa na aplikację portalową. Dziękuję wszystkim za komentarze. Propozycji było bardzo dużo. Wybór padł na nazwę, która jest...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_7" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_7" checked="checked" value="128"><label for="chkTagsList_7">programowanie</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



Prace nad aplikacją nadal trwają. Dziękuję, za docenienie tej serii i oddane głosy na moje  *wpisy*  w [marcowym konkursie blogowym](http://www.dobreprogramy.pl/Cebula/Nagradzamy-najlepszych-blogerow-marca-2016,72349.html) ;)

Jak już zapewne zauważaliście, została wybrana nazwa na aplikację portalową. Dziękuję wszystkim za komentarze.[ Propozycji było bardzo dużo](http://www.dobreprogramy.pl/djfoxer/Konkurs-na-nazwe-aplikacji-dobreprogramy.pl-a-takze-niesforny-Visual-Studio,72207.html). Wybór padł na nazwę, która jest prosta i wpadająca w ucho, a dodatkowo bardzo sprytnie kojarzy się z portalem:  
<blockquote>
<p>DePesza </p>
</blockquote>

Autorem  *DePeszy*  jest użytkownik: [Czajo](http://www.dobreprogramy.pl/Czajo). 
Gratuluję i dziękuję za wzięcie udziału w zabawie. Prócz klucza na Steam do gry  *Murdered: Soul Suspect*  dodatkowo dorzucam jeszcze klucz do gry  *Arma: Gold Edition* . 

Pozostałe wyróżnione osoby:


  * [Vidivarius](http://www.dobreprogramy.pl/258340,Vidivarius,Uzytkownik.html) -  *The Last Remnant* 


  * [sir_lucjan](http://www.dobreprogramy.pl/sir_lucjan) -  *Overlord + Overlord Raising Hell (Expansion)* 


  * [Over F.A.](http://www.dobreprogramy.pl/418183,Over-FA,Uzytkownik.html) -  *Life Is Strange - Episode 1* 


  * [Qoo](http://www.dobreprogramy.pl/178054,Qoo,Uzytkownik.html)  -  *Hospital Tycoon* 




Gratuluję i proszę o kontakt na prv :)



## Raport z prac


Tworzenie aplikacji idzie powolutku, ale cały czas idę do przodu. Przyznaję, że platforma Universal Windows Application jest jeszcze bardzo młoda i ma zauważalne choroby wieku dziecięcego.



### Pierwsza wersja testowa już w drodze


Z racji tego, iż dodawanie aplikacji do Windows Store bywa długie, postanowiłem już rozpocząć certyfikację aplikacji. Dostęp do DePeszy (fajna nazwa :D ) nie będzie jeszcze otwarty (nie znajdziecie jej w sklepie). Instalacja stanie się możliwa dopiero po otrzymaniu specjalnego linku do marketu. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-21-_45_/g_-_608x405_-_-_72467x20160421010258_0.PNG)



Pierwsza,  *ukryta* , wersja w markecie jest  testem certyfikacji i liczę na to, że kolejne aktualizacje będą przechodziły szybciej. Mam również takie wrażenie, że całość była znacznie krótsza w porównaniu do marketu Windows Phone i Windows 8.x, ale to może moja pamięć płata figle.



### Windows 10 - poligon doświadczalny





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-21-_45_/g_-_608x405_-_-_72467x20160421011850_0.gif)



Tworząc aplikację napotkałem na kilka trudności, które spędziły mi sen z powiek. Co najgorsze, czasem okazuje się, że nasz problem nie wynika z braku dostatecznej wiedzy, a z... błędów w kodzie systemu...

Zamarzyłem sobie, że powiadomienia będą miały własne, niesystemowe dźwięki w aplikacji. Mała rzecz, a okazuje się, że nie do końca wszystko w systemie jeszcze działa. 

Konfiguracja jest prosta, dodajemy do xmla, definiującego powiadomienie tag audio i ścieżkę, np:


```csharp
<audio src="ms-appx:///Assets/Sounds/alert_1.mp3" />
```


Możemy skorzystać także z różnych systemowych dźwięków. Poprzez dodanie do  *scr*  wartości np.  *ms-winsoundevent:Notification.Mail*  czy ms- *winsoundevent:Notification.Looping.Alarm* . Niestety nie do końca wszystko działa.

Na Windows 10 Mobile problemów nie ma zupełnie, ale na desktopie z Windows 10 niestety już tak nie jest kolorowo. Systemowe dźwięki odtwarzają się tylko niektóre i są inne, niż analogiczne na telefonie. Dodatkowo ktoś z MS w swoim poradniku do tworzenia powiadomień przyznał się (w czeluściach komentarzy), że zapomnieli dodać obsługę  własnych dźwięków na desktopie zdefiniowanych przez aplikację (na smartfonie wszystko działa). Prace nad znalezieniem buga trwają... Nie pytajcie ile na tym czasu spędziłem, zanim znalazłem komentarz odnośnie błędu...



### Z serii ciekawe dodatki - NotificationsExtensions



Tutaj taki mały tip, powiadomienie toast w Windows 10 definiuje się jako xml i warto użyć dodatku [NotificationsExtensions](https://github.com/WindowsNotifications/NotificationsExtensions), dzięki czemu zamiast pisać gołego xmla:


```csharp

string toastVisual =
$@"<visual>
  <binding template='ToastGeneric'>
    <text>{title}</text>
    <text>{content}</text>
    <image src='{image}'/>
    <image src='{logo}' placement='appLogoOverride' hint-crop='circle'/>
  </binding>
</visual>";

```


można ładnie zdefiniować całość za pomocą obiektów:

```csharp

ToastVisual visual = new ToastVisual()
{
    TitleText = new ToastText()
    {
        Text = title
    },
 
    BodyTextLine1 = new ToastText()
    {
        Text = content
    },
 
    InlineImages =
    {
        new ToastImage()
        {
            Source = new ToastImageSource(image)
        }
    },
 
    AppLogoOverride = new ToastAppLogo()
    {
        Source = new ToastImageSource(logo),
        Crop = ToastImageCrop.Circle
    }
};

```


Bardzo ułatwia i pomaga.



### Błędy i niedoróbki w DePeszy


Aplikacja działa już całkiem nieźle od kilku dni. W końcu udało się zsynchronizować pobieranie powiadomień z głównej aplikacji i zadania w tle (jest to zupełnie niezależny wątek systemowy) do jednego miejsca. Spróbuję w wolnej chwili sprawdzić, jak działać będzie Storage Roaming, który jest synchronizowany pomiędzy różnymi urządzeniami. Zatem pobrane powiadomienia na desktopie, będą widoczne również na smartfonie. Wówczas coś więcej o tym napiszę.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-21-_45_/g_-_608x405_-_-_72467x20160421015248_0.PNG)



Trochę prac wymaga jeszcze lista powiadomień pod kątem różnych zachowań (usunięcie/przeczytanie powiadomienia), aby całość była bardziej intuicyjna. Również wyskakujące informacje z procesu w tle jeszcze nie mają obsługi otwierania linku www do źródła.



## Pierwszy etap prac niedługo można będzie zamknąć


Pomimo kilku uwag, aplikacja spełnia swoje podstawowe założenie. Można się zalogować, pobrać powiadomienia, a w tle zaciągane są bieżące notyfikacje. W przypadku, gdy przyjdzie nowa informacja, pojawia się okienko z opisem, z którego można otworzyć stronę www (jeśli pochodzi z procesu głównego). 

Z listy powiadomień szybko oznaczymy i otworzymy notyfikację jako przeczytaną, a w kolejnym kroku możną ją również usunąć. Zmiany zapisywane są lokalnie, jak i na serwerze portalu.

Myślę, że do końca kwietnia aplikacja w wersji alfa/beta pojawi się w markecie dla każdego. Mam nadzieję, że tak się stanie i nie będzie dużo narzekań na niedociągnięcia, które zapewne na bieżąco postaram się naprawiać :)



<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-4-21-_45_/g_-_608x405_-_-_72467x20160421010253_0.png)

