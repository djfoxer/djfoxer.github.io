---layout:     post
title:      &quot;Co wAppStore?&quot; - coś więcej niż Marketplace dla Windows Phone
date:       2012-04-03 23:32:00
summary:    &quot;Co wAppStore?&quot; - nic ciekawego :)Oczywiście nie będzie to opis AppStora Appla. Program wAppStore to alternatywny (kolejny) Marketplace, gdzie znajdziemy aplikacje dla Windows Phone.Teoretycznie jest to program, bardzo zbliżony do Bazaar, który opisywałem już wcześniej. Znajdziemy w nim ap...
categories: oprogramowanie porady urządzenia mobilne
---



&quot;Co wAppStore?&quot; - nic ciekawego :)

Oczywiście nie będzie to opis AppStora Appla. Program wAppStore to alternatywny (kolejny) Marketplace, gdzie znajdziemy aplikacje dla Windows Phone.Teoretycznie jest to program, bardzo zbliżony do [Bazaar](http://wp-bazaar.com), który [opisywałem już wcześniej](http://www.dobreprogramy.pl/djfoxer/Bazaar-alternatywny-Windows-Phone-Marketplace-z-PC,30433.html). Znajdziemy w nim aplikacje, które nie znalazły się w oficjalnym Marketplace Microsoftu. Czyli kolejny zbiór aplikacji, które możemy zainstalować w naszym odblokowanym urządzeniu z Windows Phone. 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_608x405_-_-_31311x20120402180053_0.png



Nie jest jednak nastawiony on tylko na aplikacje homebrew, jak Bazaar, gdyż ma tych apliakcji zaledwie 5... wAppStore, jest przeglądarką aplikacji również z oryginalnego Marketplace. Co ciekawe! Możemy wyszukiwać, zarówno w samym, oficjalnym Marketplace Microsoftu, ale również w hubach poszczególnych producentów urządzeń! Ba! Nie tylko huby producentów urządzeń (jak Nokia, czy HTC), istnieje możliwość przejrzenia hubów dla... sieci komórkowych (O2, AT&amp;T)! 




## Pustki wAppStore?



Nie oszukujmy się, wAppStore posiada obecnie 5 (!) aplikacji homebrew (w tym ciekawy eksplorator plików). Siła nie tkwi głównie w tego typu programach. wAppStore służy głównie za zamiennik Marketplace, gdzie można ściągnąć programy, bez względu na kraj na jakie zarejestrowane jest konto Live. Dzięki temu, zyskujemy dostęp do aplikacji, wcześniej nam niedostępnych. Ale to nie wszystkie ciekawostki...

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_288x192_-_-_31311x20120403225151_0.jpg

[join])

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_288x192_-_-_31311x20120403225158_0.jpg





## Dostęp do hubów producentów i... operatorów sieciowych!



Opisywałem niedawno[ jak można dostać się do hubów producentów urządzeń](http://www.dobreprogramy.pl/djfoxer/Aplikacje-OEM-z-Marketplace-dla-wszystkich-urzadzen,30608.html). Było to jednak dość mocno kłopotliwe. Należało za każdym razem, gdy chleliśmy zmienić huba, podłączyć urządzenie do PC, wgrać aplikację i zrestartować urządzenie. Cóż, dzięki wAppStore nie jest to już potrzebne. Program posiada możliwość pobrania i zainstalowania aplikacji dostępnej jedynie dla wybranych urządzeń. Ale to nie koniec. Okazuje się, iż oddzielne aplikacje posiadają również operatorzy komórkowi! Nie ma tam &quot;szału&quot;, ale możliwe, że w przyszłości pojawią się unikatowe aplikacje od operatorów sieciowych. Polecam przejrzeć ofertę!

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_288x192_-_-_31311x20120403225203_0.jpg

[join])

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_288x192_-_-_31311x20120403225210_0.jpg



)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_288x192_-_-_31311x20120403231214_0.jpg

[join])

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_288x192_-_-_31311x20120403231220_0.jpg



Cześć aplikacji dedykowanych dla urządzeń konkretnych producentów sprzętu (jak np. genialna Nokia Drive), nie uruchomi się  na innych urządzeniach. Nie jest jednak to do końca prawdą. Wystarczy jedynie zmienić dwa wpisy w rejestrze!

W gałęzi rejestru:


```html
HKEY_LOCAL_MACHINE \ System \ Platform \ DeviceTargetingInfo
```


zmienić wpis identyfikujący producenta:


```html
OemName
```


zmienić na np. NOKIA

a wpis identyfikujący model:


```html
MODeviceName
```


zastąpić, no niech pomyślę, np. Lumia 800

I już dostajemy dostęp do Nokia Drive :)



## Wymagania



Aby móc skorzystać z wAppSotre, należy posiadać odblokowany telefon. Ze względu na to, iż aplikacje instalowane są poprzez wAppStore, musimy mieć, albo custom ROM, albo [WP7 Root Tools](http://www.dobreprogramy.pl/djfoxer/Rootowanie-w-Windows-Phone-dla-wszystkich,31248.html) do nadawanie praw roota dla aplikacji. Co ciekawe, dzięki WP7 Root Tools, bez custom ROMów można w pełni korzystać także z Bazaar! Instalujemy aplikacje homebrew bezpośrednio z Bazaar, bez podłączania urządzenia do PC!

Dodam tylko, iż wAppStore posiada również całkiem udany klient dostępny na PC, z poziomu którego można zarządzać zainstalowanymi aplikacjami, wyszukiwać w hubach itp. Wymaga on jednak dopracowania, gdyż miejscami interface bywa kapryśny (przeglądanie aplikacji na urządzeniu, potrafi zacząć żyć własnym życiem).

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_608x405_-_-_31311x20120403225216_0.png



)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-4-3-_142_/g_-_608x405_-_-_31311x20120403225223_0.png




wAppStore jako aplikacja agregująca aplikacje homebrew nie zachwyca. Jednakże, możliwość instalowania aplikacji niedostępnych w naszym regionie i programów dedykowanych dla poszczególnych urządzeń producentów lub sieci komórkowych, sprawia, że wAppStore jest warty uwagi. Idealnie jako rozszerzenie Bazzar. Zachęcam do testów.)