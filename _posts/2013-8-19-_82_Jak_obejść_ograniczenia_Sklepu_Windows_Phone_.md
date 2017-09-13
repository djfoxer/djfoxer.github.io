---
layout:     post
title:      Jak obejść ograniczenia Sklepu Windows Phone?
date:       2013-08-19 16:14:00
summary:    Każdy z producentów ma własne unikalne aplikacje w sklepie Windows Phone, co więcej, ograniczone często do konkretnych modeli urządzeń (np. Nokia Pro Cam ograniczona do modeli 92x i 1020). Zatem teoretycznie nie zainstalujemy aplikacji od Noki na HTC i na odwrót, także dedykowanej aplikacji do zdjęć...
categories: <input id="chkTagsList_3" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_3" checked="checked" value="8"><label for="chkTagsList_3">oprogramowanie</label> <input id="chkTagsList_6" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_6" checked="checked" value="64"><label for="chkTagsList_6">porady</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



Każdy z producentów ma własne unikalne aplikacje w sklepie Windows Phone, co więcej, ograniczone często do konkretnych modeli urządzeń (np. [Nokia Pro Cam](http://www.windowsphone.com/pl-pl/store/app/nokia-pro-cam/bfd2d954-12da-415c-ad99-69a20f101e04) ograniczona do modeli 92x i 1020). Zatem teoretycznie nie zainstalujemy aplikacji od Noki na HTC i na odwrót, także dedykowanej aplikacji do zdjęć dla Lumii 920 nie pobierzmy na Lumię 820. Okazuje się jednak, że można to w prosty sposób obejść, bez magicznej wiedzy.




## Przygotowania do pracy



Aby móc działać w jakikolwiek sposób, należy pobrać program [Fiddler](http://fiddler2.com/get-fiddler). Dzięki tej aplikacji będziemy w stanie monitorować ruch jaki generuje nasze urządzenie z Windows Phone. Kiedy już zainstalujemy Fiddlera, czas na konfigurację:



  * Musimy sprawdzić nasze IP, na którym zainstalowany jest Fiddler. Najszybciej wykonamy to z linii poleceń. Skrótem  *Windows+R*  otwieramy okno  *Uruchamianie* , wpisujemy w nim  *cmd* , aby uruchomić linię poleceń. Wpisujemy komendę  *ipconfig*  i sprawdzamy nasz adres IP.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_608x405_-_-_45753x20130818142007_0.png)





  * Komputer, na którym jest Fiddler, pełnić będzie rolę proxy. Zatem ustawmy w Windows Phone odpowiednie opcje. Połączmy się z sieci WiFi (w której już jest obecny komputer z Fiddlerem) i poprzez przytrzymanie palca na nazwie sieci, dodajmy proxy.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_288x192_-_-_45753x20130818142007_0.jpg)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_288x192_-_-_45753x20130818142005_0.jpg)



Adres IP ustawimy taki, jaki jest na komputerze z Fiddlerem, zaś nr portu wpisujemy:  *8888*  (domyślnie dla Fiddlera).






  * Czas na uruchomienie Fiddlera. W menu opcji  *Tools->Fiddler Options...*  w zakładce  *Connections* , zaznaczyć należy  *Allow remote computers to conect* .


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_608x405_-_-_45753x20130818142530_0.png)






 


## Analiza podglądu



Już na tym etapie wszelki ruch sieciowy wykonywany z poziomu telefonu, powinien być wychwytywany przez Fiddlera (jeśli tak nie jest, sprawdź czy opcja  *File->Capture Traffic*  jest zaznaczona). Warto teraz wyczyścić okno Fiddlera (ikona krzyżyka i wybieramy  *Remove all* ). 

Wejdźmy na urządzeniu z Windows Phone do Sklepu i wybierzmy jakąś aplikację do wyświetlenia. W oknie Fiddlera pojawi się m.in. log z hostem  *marketplaceedgeservice.windowsphone.com* . Jest to link, który został wysłany ze smartofnu do Sklepu. Zobaczmy jak wygląda taki przykładowy adres:

http://marketplaceedgeservice.windowsphone.com/v8/catalog/apps/9c3e8cad-6702-4842-8f61-b8b33cc9caf1?os=8.0.10211.0&cc=PL&oc=&lang=pl-PL&hw=50700000&dm=RM-825_eu_poland_295&oemId=NOKIA&moId=&cf=00-0

Szybko zauważymy:


  * ID aplikacji (to ten długi GUID).


  * Wersję systemu urządzenia - znacznik  *os* 


  * Język i region - znacznik  *cc*  i  *lang* 


  * Wersję sprzętu - znacznik  *hw* 


  * Wersja firmwareu (określa model urządzenia i operatora) - znacznik  *dm* 


  * Producent/OEM - znacznik  *oemId* 



Oczywiście to nie wszystkie parametry, jakie są wysyłane, ale te które na daną chwilę mogę się nam przydać.



## Jak podmienić wartości?



Wiemy już jak wygląda link do Sklepu i co w nim jest przesyłane. Jak teraz  *w locie*  podmienić wartości na takie, jakie zechcemy ustawić? Użyjemy tu Fiddlera. Można to osiągnąć w dwojaki sposób. Z poziomu GUI (zakładka  *AutoResponder*  i ustawienie reguł) lub w skrypcie. Opcja pierwsza jest najprostsza, ale najmniej uniwersalna i konfigurowalna, druga zaś ma większe możliwości i nią się właśnie zajmiemy:



  * Skrótem  *Ctrl+R*  otwieramy plik z regułami dla Fiddlera.


  * Znajdujemy linijkę: 
```c#
static function OnBeforeRequest(oSession: Session) {
```
 


  * za tą linijką wklejamy kod:


```c#
if(oSession.uriContains("_ORG"))
{
	oSession.url = oSession.url.Replace("_ORG"","_ZMIANA");
}
```

Powyższy kod sprawdza, czy w url znajduje się szukany ciąg, jeśli tak jest, podmienia go.

 *_ORG*  jest szukanym elementem w stringu,
 *_ZMIANA*  to wartość na jaką chcemy zamienić. 




  * Po edycji zapisujemy plik.






## Wykorzystanie



Znamy wygląd url wysyłanego do Sklepu oraz z czego się składa, teraz przyszedł czas na kilka przykładów wykorzystania tej wiedzy.



### Pobieranie aplikacji OEM od innego producenta, niż producent urządzenia


Sprawa jest prosta. Posiadamy np. Lumię od Nokii, a chcemy pobrać aplikację [Photo Enhancer](http://www.windowsphone.com/pl-pl/store/app/photo-enhancer/8e17bc66-2bb2-df11-8a2f-00237de2db9e), która dedykowana jest tylko dla urządzeń od HTC. Naszym celem jest podmiana producenta OEM, jaki jest doklejany do url. Oto co należy zrobić:


  * Wykonać wszystkie kroki opisane w punkcie  *Przygotowania do pracy* 


  * W kodzie z punktu  *Jak podmienić wartości?*  ustawiamy:


  *  *_ORG*  -  *NOKIA* 
 

  *  *_ZMIANA*  -  *HTC* 








  * Wchodzimy bezpośrednio do Sklepu z linku: [Photo Enhancer](http://www.windowsphone.com/pl-pl/store/app/photo-enhancer/8e17bc66-2bb2-df11-8a2f-00237de2db9e)


  * 
Otwiera się okno Sklepu...


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_288x192_-_-_45753x20130818153520_0.jpg)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_288x192_-_-_45753x20130818154033_0.png)


... i instalujemy aplikację.
  






Dla ułatwienia podaję listę z linkami aplikacji od konkretnych producentów:



  * Nokia - [link](http://www.windowsphone.com/en-in/store/oem/apps-from-nokia?oemid=nokia)


  * Samsung - [link](http://www.windowsphone.com/en-us/store/oem/samsung-zone?oemid=Samsung)


  * HTC - [link](http://www.windowsphone.com/en-in/store/oem/htc-apps?oemid=htc)





### Instalacja aplikacji dostępnych tylko dla określonych urządzeń


Na pewno wszyscy kojarzą aplikację [Nokia Pro Cam](http://www.windowsphone.com/pl-pl/store/app/nokia-pro-cam/bfd2d954-12da-415c-ad99-69a20f101e04), która wraz z aktualizacją Amber, została udostępniona tylko dla urządzeń Lumia z serii 92x oraz 1020. Nic nie stoi jednak na przeszkodzie, aby pobrać Nokia Pro Cam np. na Lumię 820. W tym celu, podmienimy model urządzenia, jaki przesyłany jest w url. Poszczególne etapy wyglądają następująco:  



  * Wykonać wszystkie kroki opisane w punkcie  *Przygotowania do pracy* 


  * Zapisujemy nazwę firmwareu urządzenia. Można to zrobić poprzez analizę linka wysyłanego do Sklepu lub prościej, w opcjach:  *Ustawienia->info+dodatki* , klikamy na  *więcej*  i spisujemy nazwę z pola  *Manufacturer Name* .


  * W kodzie z punktu  *Jak podmienić wartości?*  ustawiamy:


  *  *_ORG*  -  *nazwa_z_manufacturer_name* 
 

  *  *_ZMIANA*  -  *RM-877_nam_att_205*  (będziemy przestawiać się jako Lumia 1020 od ATT)





  * Wchodzimy bezpośrednio do Sklepu z linku: [Nokia Pro Cam](http://www.windowsphone.com/pl-pl/store/app/nokia-pro-cam/bfd2d954-12da-415c-ad99-69a20f101e04)


  * 
Otwiera się okno Sklepu...


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_288x192_-_-_45753x20130818153518_0.jpg)

[join]

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-8-19-_82_/g_-_288x192_-_-_45753x20130818154029_0.png)


... i instalujemy aplikację.
  






## Kilka uwag



W ten sposób mamy dostęp do wszelakich aplikacji umieszczonych w Sklepie Windows Phone. Na koniec kilka uwag i porad:



  * Niektóre aplikacje (jak Hub od HTC z zegarkiem w kafelku) wymagają dodatkowych sterowników/plików, stąd nie będą w pełni funkcjonalne na innych, niż dedykowane urządzenia.


  * W ten sposób można również mieć dostęp do aplikacji ograniczonych przez region/język. Wówczas należy ustawić proxy na zagraniczne (może być niebezpieczne!).


  * Internet Explorer i Sklep na Windows Phone posiadają cache z wynikami zwracanymi z serwera, stąd podmiana nie zawsze będzie natychmiast widoczna.


  * W edytowany pliku w Fiddlerze można dodawać własny kod w C#.


  * Pamiętajmy, aby wyłączyć proxy po zakończonej pracy!



Miłego grzebania! :)