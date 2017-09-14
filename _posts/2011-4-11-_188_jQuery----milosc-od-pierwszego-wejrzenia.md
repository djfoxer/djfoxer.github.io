---
layout:     post
title:      jQuery  - miłość od pierwszego wejrzenia!
date:       2011-04-11 18:42:00
summary:    .......##..#######..##.....##.########.########..##....##.......##.##.....##.##.....##.##.......##.....##..##..##........##.##.....##.##.....##.##.......##.....##...####.........##.##.....##.##.....##.######...########.....##....##....##.##..##.##.##.....##.##.......##...##......##....##....##.##....##..##.....##.##.......##....##.....##.....######...#####.##..#######..########.##........
categories: programowanie
slug: jQuery--milosc-od-pierwszego-wejrzenia,24258.html
---



[code].......##..#######..##.....##.########.########..##....##
.......##.##.....##.##.....##.##.......##.....##..##..##.
.......##.##.....##.##.....##.##.......##.....##...####..
.......##.##.....##.##.....##.######...########.....##...
.##....##.##..##.##.##.....##.##.......##...##......##...
.##....##.##....##..##.....##.##.......##....##.....##...
..######...#####.##..#######..########.##.....##....##...
[/code]

jQuery - write less, do more

Chciałbym podzielić sie z Wami, pięknem jQuery [1] (dalej jq). Kilka miesięcy temu [skandyn dodał wpis](http://www.dobreprogramy.pl/skandyn/Framework-jQuery,20575.html), w którym przedstawił pobieżnie, jak zrobić prosta galerię z jq, bez zagłębiania i wstępnej prezentacji geniuszu jq:). Tutaj chciałbym ogólnie zaprezentować jq, dla niewtajemniczonych (są jeszcze tacy?:)).

Czym jest jq? Można powiedzieć, iż jest to biblioteka do Java Script (dalej js), która, pomaga w obsłudze js i drzew DOM. Jednakże robi to w tak finezyjny sposób, iż po pewnym czasie korzystania z niej, dochodzimy  do wniosku, iż życie bez jq było szare i nudne :)

Świetnie oddaje to motto jq: "write less, do more". Niby można to samo zrobić w czystym js (jasne, że można, jq to js:P), ale ilość i zamotanie kodu w czystym js byłoby niesamowite. Po jakiś większych wygibasach z jq, dochodzę do wniosku, iż pisanie kodu w czystym js bez jq mija sie z celem. Tracimy nie tylko czas, a co ważne w tworzeniu czegos "pro", kasę! 

Potęgę jq odkrył juz nawet M$, zamieszczając jq, jako domyślna bibliotekę do MVC. W sumie MVC to po części jq :P I taka o to para MVC + jq staje sie poezja pisania stron www. Wystarczy porównać nieszczęsne, brudne i brzydkie ASP. Ah ok, sorki, najłatwiej to nawymyślać na ASP, przyznaje sie :P. Ale jak tu o tym nie wspomnieć przy MVC :P
Oczywiście jq działa z każdym frameworkiem, php, jsf, python, co sobie zażyczycie :) Co jest ważne, jest on zgodny z rożnymi silnikami do renderowania www. Wiec nie trzeba robić czasem obejść dla rożnych wersji np. IE. Ale to nie powinno nikogo dziwić. 

jQuery  - na szybkiego

Nauka jq jest szybka i bezproblemowa. W sieci jest bardzo dużo tutoriali do jq. Od czego należało by zacząć naukę. Na pewno od wstępu do czystego js :) Załóżmy, że już macie to za sobą :P Co jest najważniejsze w jq? Selektory! Czyli składania do jq, która zgarnia elementy html i pozwala operować na nich. Selektory mogą zaczynać się od:
 - ".nazwa" - co oznacza, iż szukamy wszystkich elementów które mają klasę z nazwą class="nazwa" 
- "#nazwa" - w tym przypadku szukamy elementu o id="nazwa".
- "nazwa" - wówczas szukamy elementów typu nazwa

html do testów:


```html
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>X</title>
    <script src="http://code.jquery.com/jquery-1.5.2.min.js"
    type="text/javascript"></script>
  </head>
  <body>
    <script type="text/javascript">
	$(document).ready(function () {
		alert($("#tabela_1 option:selected[value='czerowny']").size());
		alert($("select[title^='ok']").size());
		alert($("#last ~ tr").hide());
	});</script>
    <table id="tabela_1">
		<tr>
			<td>
				<select title="ok_1">
					<option value="czerowny" selected="selected">czerowny</option>
					<option value="czarny">czarny</option>
				</select>
			</td>
		</tr>
		<tr id="last">
			<td>
				<select  title="ok_2">
					<option value="czerowny">czerowny</option>
					<option value="czarny" selected="selected">czarny</option>
				</select>
			</td>
		</tr>
		<tr>
			<td>
				<select title="x_3">
					<option value="czerowny" selected="selected">czerowny</option>
					<option value="czarny">czarny</option>
				</select>
			</td>
		</tr>
    </table>
  </body>
</html>
```


Co ciekawe selektory mogą być bardzo rozbudowane. 
I tak, np. jeśli:
-szukamy w tabeli id="tabela_1" selektora, który ma zaznaczona opcje "czerwony" nasz selektor w jq wygląda następująco (size() zwraca ilość elementów wybranych przez selektora):

```js
$("#tabela_1 option:selected[value='czerwony']").size()
```

- jeśli zaś chcemy pobrać wszystkie selektory z id title rozpoczynającym sie od ok:

```js
$("select[title^='ok']").size()
```

-ale tylko co drugi wynik (od indeksu 0):

```js
$("select[title^='ok']:even").size()
```

- i jeszcze chcemy ukryć następne elementy tr po elemencie tr o id="last":

```js
$("#last ~ tr").hide()
```



Selektory mają wiele dodatkowych elementów i można je łączyć. Na wybranych elementach możemy wykonywać wiele operacji, ukrywania, zwracania danych, podstawiania, edycja cssów/klas, wrzucania dynamicznie kodu html, właściwie wszystko co nam przyjdzie do głowy. Ze względu n to, iż jest tego baaardzo dużo zachęcam to zapoznania się z dokumentacją jq [1] .

To jest również piękne, iż do tych samych rezultatów w jq można dojść w różny sposób. Każdy może zrobić to tak w jaki sposób będzie chciał. 

Jeśli już wspomniano o dynamicznym wrzucaniu htmla. Bardzo łatwo możemy podczepić własne eventy do kontrolek html np.:



```js
$('#button').click(function() {
  alert("click!");
});
```


Gdyby ktoś chciał pobrać dane postem ze np. webservsu: 

```js
$.ajax({
        type: "POST",
        url: "Service/DataService.asmx/GetData",
        data: { Id: 1 },
        contentType: "application/json; charset=utf-8",
        dataType: "json",
        success: function (msg) {
            alert(msg.value);
        },
        error: function (msg) {
		alert("ups");
        }
    });
```


Biblioteka jq posiada jeszcze wiele, wiele funkcji i ma wręcz nieograniczone możliwości :)



## Morze pluginów


Oczywiście pisząc w jq nie sposób nie skorzystać z chyba nieskończonej ilości pluginów. Z czego obowiązkowym przykładem jest jQueryUI. Biblioteka do graficznych elementów wykorzystująca potęgę jq. To co zostało nam dane przez Twórców JQUI [2]  zasługuje na największe pochwały. Otrzymujemy 8 przepięknie stworzonych kontrolek, z  wieloma możliwościami, które w bardzo prosty sposób możemy rozbudowywać oraz świetną dokumentacje. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-4-11-_188_/g_-_608x405_-_-_24258x20110410231307_1.png)
 
 *Rys. 1 jqUI*   

Chociaż jedno zdanie muszę napisać o jQueryValidate. Plugienie do walidacji formularzy, z którego skorzystał MS w MVC. Jest prosty i efektywny. „Lubię to”!

Moimi pupilkiem jest jqGrid [3],[4]  . Plugin, który udostępnia nam grida ze stronicowaniem, wyszukiwaniem, sortowaniem, dodawaniem własnych przycisków, dynamicznym ładowaniem danych za pomocą ajaxa, dodawanie własnych typów komórek,... Nie wyobrażam sobie teraz jakiegoś np. Admin Panelu bez tej wtyczki.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-4-11-_188_/g_-_608x405_-_-_24258x20110410231307_2.png)

 *Rys. 2 jqGrid*   



## Testy


Dzięki stronie [5]  , każdy może przetestować szybkość działania jq i porównać wyniki z innymi frameworkami. Test oparty jest na selektorach. Moje wyniki:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2011-4-11-_188_/g_-_608x405_-_-_24258x20110411173518_3.png)

 *Rys. 3 Wyniki porównania frameworków*  

Interpretacja jest prosta :) Jq jest w czołówce, przy czym różnice nie są duże pomiędzy najszybszymi frameworkami. Na uwagę zasługuje rewelacyjny wynik Chrome oraz zaskakująco dobry wynik IE. FF niestety zostaje w tyle, no ale można było się tego spodziewać. Niestety wyniki są niedeterministyczne.  Test uruchomiony ponownie, daje inne rezultaty, jednakże nie są to różnice duże. 



## Podsumowanie


Jeśli jeszcze nie znasz jq to zachęcam do przetestowania. Framework jest szybki, prosty w nauce oraz ma rewelacyjną dokumentację. Jeśli doda się do tego olbrzymią bibliotekę darmowych pluginów, faktem staje się stwierdzenie, iż jq jest tym czego poszukujemy w pracy z js :)



## Pozdrawiam.








## Powiązane


[1] [http://jquery.com/ - jQuery Home](http://jquery.com/) 
[2] [http://jqueryui.com/ - jQueryUI Home](http://jqueryui.com/) 
[3] [http://www.trirand.com/blog/ - jqGrid](http://www.trirand.com/blog/) 
[4] [http://trirand.com/blog/jqgrid/jqgrid.html - jqGrid Demo](http://trirand.com/blog/jqgrid/jqgrid.html) 
[5] [http://mootools.net/slickspeed/ - test frameworków js](http://mootools.net/slickspeed/) 
