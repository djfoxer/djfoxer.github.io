---
layout:     post
title:      jQuery plugin - własna wtyczka od podstaw
date:       2012-01-26 20:49:00
summary:    W tym krótkim wpisie, przedstawię jak szybko można napisać własny plugin do jQuery. Z racji tego, iż jest to obecnie jeden z najbardziej popularnych frameworków JavaScriptowych, znajomość tworzenia rozszerzeń jest bardzo przydatna.Nasz pluginW celu uniknięcia tworzenia sztuki dla sztuki, stworzona w...
categories: internet porady programowanie
---



W tym krótkim wpisie, przedstawię jak szybko można napisać własny plugin do jQuery. Z racji tego, iż jest to obecnie jeden z najbardziej popularnych frameworków JavaScriptowych, znajomość tworzenia rozszerzeń jest bardzo przydatna.



### Nasz plugin


 *W celu uniknięcia tworzenia sztuki dla sztuki, stworzona wtyczka będzie coś robić. Jej zadaniem będzie zmiana tła w środku elementu, po kliknięciu na tym obiekcie. Jako parametry przyjmować będzie dwa kolory, które co kliknięcie będą się zmieniać.* 



## Baza



Każdy plugin dla jQuery składa się z bazy, która zawsze jest identyczna dla każdej wtyczki, bez względu na to w jaki sposób będzie dalej tworzona.

Pierwszym krokiem jest dostarczenie naszemu pluginowi dostępu do $ oraz zapewnienie unikalności nazw i niekolidowania z innymi wtyczkami:



```js

(function($) {
	//baza pod plugin
})(jQuery	

```


Teraz przyszedł moment aby dodać do kodu funkcję, w której nasz plugin będzie działał:


```js

(function($) {
	$.fn.changeColor = function() {
		//ciało naszego pluginu
	}
})(jQuery);

```


Na tym etapie nazywamy nasz plugin. W tym przypadku będzie to changeColor. Już w tym momencie nasz plugin istnieje, mimo, iż nic nie robi można go wywołać:


```js
$("div").changeColor();
```





## Łańcuchowość



Pluginy jQuery opierają się na zasadzie, iż każda wtyczka zwraca przetworzony/wybrany łańcuch obiektów dalej. Dzięki czemu można pisać ciąg poleceń np.:


```js

$("div").attr("data-type","slider").addClass("slider");

```


W powyższym przykładzie, ze strony wybieramy wszystkie elementy div i ustawiamy im atrybut  *data-type*  na  *slider* . Dzięki temu, iż  *attr*  zwraca łańcuch divów z dodanym atrybutem, możemy ponownie przetworzyć dane i np. dodać do każdego diva klasę  *slider* .

Łańcuchowośc zapewnimy, dzięki temu, iż plugin zwracać będzie element  *this* , czyli dane które otrzymał do przetworzenia:


```js

(function($) {
	$.fn.changeColor = function() {
		return this.each(function() {
		  //ciało naszego pluginu
		});	
	}
})(jQuery);

```
	



## Parametry wejściowe



Nasz plugin powinien przyjmować parametry wejściowe, zatem należy zapewnić taką możliwość:


```js

(function($) {
	$.fn.changeColor = function(options) {
	
		//parametry wejściowe
		var settings = $.extend( {
		  colorFirst : 'Red',
		  colorSecond : 'Green'
		}, options);
		
		return this.each(function() {
		  //ciało naszego pluginu
		});	
	}
})(jQuery);
```
	

Dzięki temu szybkiemu zabiegowi, uzyskaliśmy kilka ważnych rzeczy. Nasz plugin uzyskał możliwość inicjalizacji z	parametrami wejściowymi.  *colorFirst*  oraz  *colorSecond*  mają odpowiadające wartości domyślne, które mogę być zmienione na te które poda użytkownik. 
Możliwe wywołania:


```js

$("div").changeColor({ colorFirst : 'Blue', colorSecond : 'Black' });
//parametry domyślne
$("div").changeColor();
//ustawienie tylko jednego parametru
$("div").changeColor({ colorSecond : 'Yellow' });

```






## Metody publiczne i prywatne



Kolejny krok to dodanie metod. Jeśli nasza wtyczka ma być prosta można spokojnie zacząć kodować w ciele głównej metody pluginu. Jednakże, jeśli kod ma być bardziej złożony i dodatkowo udostępniać na zewnątrz metody, warto jeszcze chwilę poczekać. 

Poniższy schemat jest zalecany, w przypadku pluginów posiadających publiczne metody. Dzięki takiemu stworzeniu metod, nie marnujemy niepotrzebnie nazw w obrębie jQuery.


```js

(function($) {
	$.fn.changeColor = function(options) {
		
		//metoda prywatna
		function onClick(event) {
			//ciało metody prywatnej
		}
		
		//metody publiczne
		var methods = {
			swapColors: function() {
				//wystawiona metoda
			},
			destroy: function() {
				//destruktor 
			}
		};
		
		return this.each(function() {
			//ciało naszego pluginu
			if(methods[options]){	
				//wywołana metoda publiczna
				return methods[options].apply( this, arguments );
			}
			else if (typeof options === 'object' || ! options ){
				//wywołany konstruktor
				var settings = $.extend( {
				  colorFirst : 'Red',
				  colorSecond: 'Green'
				}, options);
				//inicjalizacja pluginu
				return;
			}
			else{
				//bład
				$.error('changeColor: no method: '+ options);
			} 
		});	
	}
})(jQuery);					
	
```
	

Powyżej stworzono obiekt  *methods* , zawierający metody publiczne.  *SwapColors*  jest publiczną metodą wystawioną na zewnątrz. Taki zabieg powoduje, iż do metody odwołujemy się podobnie jak ma to miejsce w pluginie jQuery UI:


```js

$("div").changeColor('swapColors');

```


Dodatkowo prywatna metoda  *onClick*  będzie użyta jedynie wewnątrz wtyczki.



## Destruktory



Pisząc plugin do jQuery, warto zadbać o to by można było nasz plugin "odinstalować". Należy zatem dodać metodę która będzie sprzątała po naszej wtyczce. W takim destruktorze warto zadbać o to, by znalazło się w nim usunięcie np. eventów, które podczepiliśmy podczas inicjalizacji lub innych danych wrzuconych do htmla. Do powyższego kodu dołączono metodę  *destroy* , wywołuje się ją podobnie jak inne publiczne metody.



## Dodawanie funkcjonalności



Możemy zatem przystąpić do dodawani funkcjonalności do naszego pluginu.
Na początek dodamy inicjalizację wtyczki:


```js

//inicjalizacja pluginu
$this = $(this);
data = $this.data("changeColor");
if(!data)
{
	data = $this.data("changeColor", settings);
	$this.bind("click", onClick);
}
$this.css("background-color", settings.colorFirst);
data.first = true;

```


Powyższy kod sprawdza, czy przypadkiem plugin dla danego elementu nie jest już jest dodany. W tym przypadku sprawdzić można, czy element posiada dane pod wybranym kluczem:  *changeColor* . W prosty sposób unikamy podwójnego inicjalizowania tego samego elementu, a także jest to świetny sposób na przechowanie parametrów wejściowych. Do elementu, podczepiliśmy metodę  *onClick* , która będzie wywoływana dla eventu odpowiadającego za kliknięcie myszką. Zmienna  *first *  będzie informować, o tym który kolor mamy ustawić jako tło.

Przyszła kolej na dodanie ciała dla funkcji  *onClick* , która podmienia tło dla klikniętego elementu;


```js

//ciało metody prywatnej
$this = $(this);
data = $this.data("changeColor");
data.first = !data.first;
$this.css("background-color", 
	data.first ? data.colorSecond : data.colorFirst);
return true;

```


Dodajmy jeszcze kod dla publicznej metody  *SwapColors* , która zamienia kolejnością tła:


```js

//wystawiona metoda
$this = $(this);
data = $this.data("changeColor");
tmp = data.colorSecond;
data.colorSecond = data.colorFirst;
data.colorFirst = tmp;

```


Ostatni krok to uzupełnienie metody dla destruktora:


```js

//destruktor
$this = $(this);
$this.unbind("click");
$this.css("background-color","");
$this.removeData("changeColor");

```


Gdy zechcemy usunąć plugin z elementu wywołujemy metodę  *destroy* . Pozbywamy się eventa dla kliknięcia na element i czyścimy wszelkie dane.



### Nasz gotowy plugin




```js

(function($) {
	$.fn.changeColor = function(options) {
		
		//metoda prywatna
		function onClick(event) {
			//ciało metody prywatnej
			$this = $(this);
			data = $this.data("changeColor");
			data.first = !data.first;
			$this.css("background-color", 
				data.first ? data.colorSecond : data.colorFirst);
			return true;
		}
		
		//metody publiczne
		var methods = {
			swapColors: function() {
				//wystawiona metoda
				$this = $(this);
				data = $this.data("changeColor");
				tmp = data.colorSecond;
				data.colorSecond = data.colorFirst;
				data.colorFirst = tmp;
			},
			destroy: function() {
				//destruktor
				$this = $(this);
				$this.unbind("click");
				$this.css("background-color","");
				$this.removeData("changeColor");	
			}
		};
		
		return this.each(function() {
			//ciało naszego pluginu
			if(methods[options]){	
				//wywołana metoda publiczna
				return methods[options].apply( this, arguments );
			}
			else if (typeof options === 'object' || ! options ){
				//wywołany konstruktor
				var settings = $.extend( {
				  colorFirst : 'Red',
				  colorSecond: 'Green'
				}, options);
				//inicjalizacja pluginu
				$this = $(this);
				data = $this.data("changeColor");
				if(!data)
				{
					data = $this.data("changeColor", settings);
					$this.bind("click", onClick);
				}
				$this.css("background-color", settings.colorFirst);
				data.first = true;
				return;
			}
			else{
				//bład
				$.error('changeColor: no method: '+ options);
			} 
		});	
	}
})(jQuery); 


```


Jak widać tworzenie pluginów do jQuery nie jest trudne. A zatem, do dzieła! :) 