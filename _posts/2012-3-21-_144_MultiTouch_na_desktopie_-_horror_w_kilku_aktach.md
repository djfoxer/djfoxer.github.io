---
layout:     post
title:      MultiTouch na desktopie - horror w kilku aktach
date:       2012-03-21 22:53:00
summary:    Niedawno miałem przyjemność (i nadal mam) pracować przy tworzeniu aplikacji na ekrany dotykowe, podłączone do zwykłych komputerów desktopowych. Całość miała być robiona w oparciu o HTML5. Systemem miał być koniecznie Windows 7 (założenia odgórne). W sumie nie było to złe rozwiązanie, gdyż multitouch...
categories: <input id="chkTagsList_7" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_7" checked="checked" value="128"><label for="chkTagsList_7">programowanie</label> <input id="chkTagsList_8" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_8" checked="checked" value="256"><label for="chkTagsList_8">urządzenia mobilne</label>
---



Niedawno miałem przyjemność (i nadal mam) pracować przy tworzeniu aplikacji na ekrany dotykowe, podłączone do zwykłych komputerów desktopowych. Całość miała być robiona w oparciu o HTML5. Systemem miał być koniecznie Windows 7 (założenia odgórne). W sumie nie było to złe rozwiązanie, gdyż multitouch na linuxie mógł sprawić dużo kłopotu,a terminy były napięte. Z racji tego, że oprócz HTML5 nie było innych wytycznych, prace ruszyły bardzo szybko...

Tak przynajmniej się wydawało. Okazuje się, że temat ekranów dotykowych z multitouchem na dektopach w oparciu o HTML5 to ciągle temat "w fazie testów". Mimo, iż ekrany dotykowe w urządzeniach mobilnych są czymś normalnym, o tyle na desktopach to temat świeży, baaardzo świeży (vide Windows 8).

W kilku podpunktach omówię, ciekawostki na jakie się natknąłem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-3-21-_144_/g_-_608x405_-_-_31092x20120321222931_0.jpg)





## Firefox - jedyny sprawiedliwy



HTML5 pociągał za sobą użycie jakiejś nowszej przeglądarki. Dzięki specyfikacji aplikacji, można było wybrać jedną, konkretną wersję przeglądarki pod jaką będziemy działać. Wybór jest ogromny. Jednakże, jak się okazało, nie było to prawdą :)

HTML5 miał służyć do bardzo atrakcyjnej prezentacji aplikacji, oraz dzięki niemu nie trzeba było się zbytnio narobić :P Dodatkowo jak pisał ostatnio [alucosoftware](http://www.dobreprogramy.pl/alucosoftware/Zmiana-paradygmatu-czyli-o-GUI-slow-kilka,30967.html) tworzenie GUI w HTML ma wiele zalet: jest szybkie i komfortowe. Wisieneczką na torcie miały być gesty multitouch (powiększanie zdjęć/obiektów itp.). Okazało się, iż ten ostatni wymóg sprawił, iż z morza przeglądarek do wyboru... została tylko jedna, Firefox. Dlaczego? :)

Przeglądarki desktopowe w większości obsługują gesty multitouch samodzielnie. O czym mowa? Dotykając dwoma palcami ekranu przeglądarki, strona www... jest automatycznie skalowana. Nie ma możliwości podpięcia się pod te eventy. Internet Explorer, Chrome, Opera, wszędzie jest zoom przy dotykaniu dwoma palcami i nie da się tego wyłączyć! Już nawet były pod uwagę brane wersje beta (Opera Next, Chrome). Nadal to samo. Nie obyło się bez testów na przeglądarkach mobilnych, które mają skompilowane wersje pod desktopy (Opera Mobile, Fennec). W tym ostatnim przypadku multitouch albo wcale nie działał lub powodował zoom (dzień dobry), albo storna skakała jak oszalała. 

Nagłówek akapitu, wskazuje zwycięzce. Jedynie w Firefoxie desktopowym nie ma automatycznego zoomowania przy dotykaniu ekranu dwoma palcami. Czyżby był to już koniec problemów z przeglądarką? O nie nie...



## Firefox - zapomniany dotyk na desktopie



Ogólnie nic nie mam do dokumentacji Mozilli. Jest świetna, wyczerpująca, ma wiele przykładów (działających na live demo!) i jest naprawdę pomocna. Jednakże....

Jeśli chodzi o eventy do multitoucha to chyba kogoś tam %^#$#%@#. Już spieszę wyjaśniać. Otóż eventy do multitocha w Firefoxe zostały zaprezentowane już w becie Firefoxa 4 (2010 rok). Nawet powstał filmik, gdzie uśmiechnięty Pan bawi się multitouchem:

[youtube=http://www.youtube.com/watch?v=GL2dwXa1_gw] 

Na stronie [MDN Touch events](https://developer.mozilla.org/en/DOM/Touch_events)  jest piękny opis eventów:



  * touchstart


  * touchend


  * touchmove


  * touchenter


  * touchleave


  * touchleave



Wszystko byłoby ok, gdyby nie to, że nie chcą one działać. Co się okazuje? Otóż w wersja desktopowa Firefoxa nadal używa... starych eventow z wersji beta Firefoxa 4....



  * MozTouchDown


  * MozTouchMove


  * MozTouchUp



(źródło: [http://hacks.mozilla.org/2010/08/firefox4-beta3/](http://hacks.mozilla.org/2010/08/firefox4-beta3/))

Ludzie... :P



## Wyrzućcie tego WebKita!



Z racji tego, iż WebKit króluje na urządzeniach mobilnych, wszelkie wtyczki do np. jQuery, związane z dotykiem, tworzone są z myślą właśnie o tym silniku. Szkoda tylko, że powoli robi się z WebKita hamulec internetu, podobnie jak było ze starym Internet Explorerem. Zaglądając do kodu CSS takiej wtyczki, otrzymujemy sieczkę prefixów  *-webkit-* . Co za tym idzie? Otóż na Firefoxie (i innych nie WebKitowych silnikach) nie uświadczymy efektów działania części wtyczek, do obsługi dotyku. Ha, nawet wtyczki multitouch pod WebKita nie działają na wersji desktopowej... bida...

Występuje to nawet w jQuery Mobile. Obecnie aktualna wersja 1.0, wszelkie animacje przejścia w CSSsie, ma zrobione tylko na WebKita (nawet animacja loadingu!). Dopiero niedawno udostępniona wersja 1.1.0 RC1, dodaje efekty dla Firefoxa. Wcześniej trzeba było samemu "kompilować" pliki js i css z repo jQuery Mobile!! 




## Szybkość działania CSSów



Będąc już przy CSSach zahaczę o temat wydajności animacji. Na małych 3"-5" ekranach, nawet 1GHz mobilne procesorki spokojnie obsłużą wymyślne przejścia w CSS3. Jednakże na 22" ekranie niektóre animacje nie są już płynne. 

Bywa, że animacja typu flow dla jQuery Mobile ([http://jquerymobile.com/demos/1.1.0-rc.1/docs/pages/page-transitions.html](http://jquerymobile.com/demos/1.1.0-rc.1/docs/pages/page-transitions.html)) potrafi skonsumować nawet 50% procesora. To dużo, szczególnie, że animacja na Firefoxie nie jest rewelacyjnie płynna (nawet po hackach związanych z włączeniem akceleracji GPU). 
To nie koniec, całkiem udana wtyczka jQTouch ([http://www.jqtouch.com/preview/demos/main/#animations](http://www.jqtouch.com/preview/demos/main/#animations)) potrafi zjeść nawet do 70% procesora przy animacjach 3D (które faktycznie mogą się podobać).


W sumie w kilku miejscach trzeba było i tak samemu, korzystając z [jQuery UI Draggable](http://jqueryui.com/demos/draggable/), dorabiać "szuranie" listą po ekranie. Dla dużych danych, CSSowe animacje nie wyrabiały...



## A jednak się udało



Mimo wielu przeciwności, efekt po wstępnej fazie, wyszedł zaskakująco dobry. Mam nadzieje, że kilka wskazówek przyda się osobom chcącym tworzyć aplikacje w HTML5 na ekrany (multi)touch pod desktopy.

 *Pamiętajcie, że wraz z nowymi wersjami przeglądarek sytuacja może ulec zmianie, oby na lepsze! :)* 