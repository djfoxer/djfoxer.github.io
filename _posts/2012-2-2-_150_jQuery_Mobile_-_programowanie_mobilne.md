---
layout:     post
title:      jQuery Mobile - programowanie mobilne
date:       2012-02-02 23:31:00
summary:    Jesteśmy świadkami przeniesienia zainteresowania użytkowników, z urządzeń stacjonarnych, na urządzenia mobilne. Coraz bardziej stają się popularne smartfony, tablety. Obecnie komputer stacjonarny staje się reliktem, czymś wygasłym. Technologie mobilne zaś, zyskują rzesze zwolenników i to one napędza...
categories: programowanie urządzenia mobilne
---



Jesteśmy świadkami przeniesienia zainteresowania użytkowników, z urządzeń stacjonarnych, na urządzenia mobilne. Coraz bardziej stają się popularne smartfony, tablety. Obecnie komputer stacjonarny staje się reliktem, czymś wygasłym. Technologie mobilne zaś, zyskują rzesze zwolenników i to one napędzają nowe technologie i nowe spojrzenie na świat. Dają one większą swobodę dla użytkowników, ale i dla developerów. Szybsze dotarcie do klienta, możliwość osiągnięcia sukcesu dla mniejszych twórców. 

Dzięki [jQuery Mobile](http://jquerymobile.com/), możemy zacząć przygodę z tworzeniem webowych aplikacji mobilnych, w prosty i przyjemny sposób, w założeniu, bez martwienia się o docelowy sprzęt.




## Czym jest jQuery Mobile?



Może warto napisać czym nie jest :) Nie jest to mobilna wersja jQuery. Jest to framework, który rozszerza oryginalnego jQuery o dodatki, które są pomocne, a czasem niezbędne, do tworzenia aplikacji webowych z poziomu urządzeń mobilnych. Zatem z jQuery Mobile będziemy tworzyć strony w HTML z tą sama biblioteką jQuery co w zwykłych, &quot;dużych&quot; stronach. 



## Co otrzymujemy?



Twórcy oddali do dyspozycji framework, który stara się być niezależny od przeglądarki w jakiej zostanie otworzona strona. Kompatybilność z urządzeniami/przeglądarkami została podzielona na kilka stopni. Większość nowych samrtfonów i tabletów oraz przeglądarek www, w 100% może wykorzystać możliwości jQuery Mobile (aktualne zestawienie na stronie: [Mobile Graded Browser Support](http://jquerymobile.com/gbs/)).



Biblioteka opiera się na HTML5 i CSS3. Otrzymujemy gotowy zestaw interfejsu, który przystosowany jest do urządzeń mobilnych, do obsługi stron palcem. Całość przypomina interface z iOSa i w działaniu sprawdza się rewelacyjnie. Wszystko jest na tyle duże, aby móc bezproblemowo trafić palcem. Tworząc stronę web pod ekrany dotykowe, wybór tego frameworku jest wręcz oczywisty. Kontrolki jakie otrzymujemy i cały UI jest bardzo bogaty. Ciekawie prezentują się również wszelkie efekty przejścia pomiędzy &quot;stronami&quot;. Mamy wrażenie, korzystania z natywnej aplikacji mobilnej.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-2-_150_/g_-_608x405_-_-_30130x20120202222432_0.png)




Biblioteka jQuery Mobile oferuje również eventy, charakterystyczne dla aplikacji na urządzenia mobilne. Warto wymienić tu: tap, czy swipe. 

Z pełnymi możliwościami można zapoznać się stronie z [demami i dokumentacją](http://jquerymobile.com/demos). Kreator tmatów graficznych dostępny jest pod tym adresem: [ThemeRoller](http://jquerymobile.com/themeroller/).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-2-_150_/g_-_608x405_-_-_30130x20120202222415_0.png)





## Przykładowa strona



Tworzenie stron jest dość proste, a efekty zaskakująco dobre.
Całość opiera się na atrybutach data z HTML5. Dzięki nim steruje się tym, jak ma zachowywać się i wyglądać dany element. &quot;Resztę&quot; robi za nas jQuery Mobile.

Przykładowy kod strony:


```html

&lt;!DOCTYPE html&gt; 
&lt;html&gt; 
	&lt;head&gt;
		&lt;meta charset=&quot;utf-8&quot;&gt;
		&lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1&quot;&gt; 
		&lt;title&gt;TEST&lt;/title&gt; 
		&lt;link rel=&quot;stylesheet&quot; href=&quot;http://code.jquery.com/mobile/1.0.1/jquery.mobile-1.0.1.min.css&quot; /&gt;
		&lt;script src=&quot;http://code.jquery.com/jquery-1.6.4.min.js&quot;&gt;&lt;/script&gt;
		&lt;script src=&quot;http://code.jquery.com/mobile/1.0.1/jquery.mobile-1.0.1.min.js&quot;&gt;&lt;/script&gt;
		&lt;script&gt;
			$(document).ready(function() {
			  $(&quot;#swipeMe&quot;).bind(&quot;swipe&quot;,function(){
				alert(&quot;swipe!&quot;);
			  });
			});
		&lt;/script&gt;
	&lt;/head&gt; 
&lt;body&gt; 
	&lt;div data-role=&quot;page&quot; id=&quot;one&quot; data-theme=&quot;c&quot;&gt;	
		&lt;div data-role=&quot;header&quot;&gt;
			&lt;a href=&quot;#&quot; data-icon=&quot;arrow-l&quot;&gt;Powrót&lt;/a&gt;
			&lt;h1&gt;Witaj&lt;/h1&gt;
		&lt;/div&gt;
		&lt;div data-role=&quot;content&quot; &gt;	
			&lt;div id=&quot;swipeMe&quot;&gt;
				&lt;span&gt;Witaj w JQuery Mobile!&lt;/span&gt;
			&lt;/div&gt;
			&lt;div&gt;
				&lt;fieldset data-role=&quot;controlgroup&quot;&gt;
					&lt;legend&gt;Wybierz :&lt;/legend&gt;
					&lt;input type=&quot;radio&quot; name=&quot;radio-choice-1&quot; id=&quot;radio-choice-1&quot; value=&quot;choice-1&quot; checked=&quot;checked&quot; /&gt;
					&lt;label for=&quot;radio-choice-1&quot;&gt;Dobre&lt;/label&gt;
					&lt;input type=&quot;radio&quot; name=&quot;radio-choice-1&quot; id=&quot;radio-choice-2&quot; value=&quot;choice-2&quot;  /&gt;
					&lt;label for=&quot;radio-choice-2&quot;&gt;Programy&lt;/label&gt;
				&lt;/fieldset&gt;
			&lt;/div&gt;
			&lt;a href=&quot;#&quot; data-role=&quot;button&quot; data-inline=&quot;true&quot;&gt;Przejdź dalej&lt;/a&gt;
		&lt;/div&gt;	
		&lt;div data-role=&quot;footer&quot;&gt;
			&lt;h4&gt;Stopka&lt;/h4&gt;
		&lt;/div&gt;
	&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;

```


A taki będzie to wyglądać w oknie przeglądarki:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-2-2-_150_/g_-_608x405_-_-_30130x20120202222320_0.png)



Strona składa się z: nagłówka ( *header* ), zawartości ( *content* ) i stopki ( *footer* ). To zaś jest stroną ( *page* ). Na jednej stronie HTML może być kilka &quot;stron&quot; ( *page* ). Dzięki czemu przejścia pomiędzy nimi mogą być płynne, z animacją &quot;przejścia&quot;, niczym w natywnej aplikacji.

Dodano event swipe do diva w standardowej funkcji  *$(document).ready()*  znanej z jQuery. jQuery Mobile, ze względu na to, iż w obrębie jednego pliku HTML, może być kilka &quot;stron&quot;, istnieje metoda  *pageInit()* , która wykonuje się dla każdej &quot;wirtualnej&quot; strony.



## Kontrowersje



Biblioteka jest bardzo rozbudowana i oferuje wiele możliwości. Mimo starań o to by była ona uniwersalna, nie jest ona w pełni zgodna ze wszystkimi przeglądarkami. Część efektów działać będzie tylko na przeglądarkach opartych o WebKita. Nie zawsze ze względu na ograniczenia innych silników, lecz ze względu na to, iż całość opiera się na CSS3, a w stylach dla niektórych efektów dodano jedynie znaczniki  *-webkit* . I tak oto mimo, że silnik Gecko wspiera rotację, w kodzie css jest tylko:  *-webkit-transform: rotate* , gdzie pod Firefoxem idealnie działa:  *-moz-transform: rotate* 

Nie ma co się spierać o UI, gdyż jest zarówno i bardzo ładny jak i funkcjonalny. Niestety nie wszystko działa jednak na urządzeniach mobilnych. Na moim Windows Phone 7.5 slidera nie można przeciągnąć. Zaś na Chromie desktopowy z Windows 7, animacje przejścia pomiędzy oknami nie były płynne. 

Sam framework bywa kapryśny. Czasem eventy dublują się i występuje tzw. &quot;bubbling&quot;, czyli wyłapywanie jednego eventu w kilku handlerach. Nie pomaga ani  *return false* , czy  *event.stopPropagation();* . Występuje to różnie i dla bindowania poprzez:  *bind* ,  *live* , czy  *on* .

Część osób narzeka również na założenie, gdzie na jednej stronie HTML występuje kilka podstron &quot;natywnych&quot;. Przechodzi się pomiędzy nimi, podobnie jak w iOS, za pomocą przesuwania. Pytanie jest, czy interface webowej aplikacji musi być podobny do natywnych aplikacji, czy nie jest to &quot;przerost formy nad treścią&quot;? Oczywiście nie jesteśmy zmuszeni do stosowania tego.

jQuery Mobile to świetny, młody projekt. Pisanie aplikacji mobilnych web, staje się prostsze, a efekty mogą zachwycić.  Rewelacyjne UI, wiele dodatkowych funkcjonalności to sprawia, iż nie można przejść obok jQuery Mobile obojętnie. Mimo kilku kontrowersji, jest to framework warty polecenia, albo chociaż przetestowania.