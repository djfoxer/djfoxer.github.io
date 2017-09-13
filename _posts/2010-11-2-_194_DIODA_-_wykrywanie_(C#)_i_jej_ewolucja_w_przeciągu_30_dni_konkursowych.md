---layout:     post
title:      DIODA - wykrywanie (C#) i jej ewolucja w przeciągu 30 dni konkursowych
date:       2010-11-02 11:59:00
summary:    Dioda konkursowa - Intel królem marketinguSam pomysł na formę konkursu z diodą jest genialny. Osoby biorące udział w &quot;zawodach&quot; co chwile musiały sprawdzać czy na stronie nie ma żółtej &quot;gwiazdeczki&quot;. To automatycznie sprawiało, iż liczba użytkowników oglądających portal, z pewnoś...
categories: programowanie hobby inne
---



Dioda konkursowa - Intel królem marketingu

Sam pomysł na formę konkursu z diodą jest genialny. Osoby biorące udział w &quot;zawodach&quot; co chwile musiały sprawdzać czy na stronie nie ma żółtej &quot;gwiazdeczki&quot;. To automatycznie sprawiało, iż liczba użytkowników oglądających portal, z pewnością wzrosła przez ten miesiąc. 

Mam nadzieje, że redakcja udostępni jakieś statystyki, odnośnie użytkowników biorących udział w konkursie i odwiedzin vortalu. A że popularność portalu wzrosła jest pewne. 

W mojej pracy przed rozpoczęciem konkursu, większość osób korzystała z dp.pl jedynie w celu ściągania aplikacji. Od kiedy rozpoczął się konkurs, każdy wiedział co kryje się pod hasłem &quot;dioda&quot;, oraz część osób na bieżąco obserwowała rankingi na stronie i niektórzy nawet założyli konta i także czekali na diodkę. Było w tym wiele emocji, nerwów i niesłychanie dużo frajdy :P 

Pytania specjalne były naprawdę wciągające. Ale to co mnie zaskoczyło i również wciągnęło to pytania normalne, z 4 odpowiedziami. Mowa tu oczywiście o słynnym pytaniu:

 *Kiedy powstał pierwszy dostępny komercyjnie procesor Intela?
Wtedy pojawił się na rynku pierwszy komputer osobisty z procesorem Intel&#174; 8088 (był to IMB PC).* 

Dyskusja jaka wywiązała się po pojawieniu się pytania chyba zaskoczyła wszystkich. Większość z nas &quot;przekopała&quot; internet w poszukiwaniu danych odnośnie pierwszych procesorów Intela. Każdy przedstawiał swoje racje i obawy. To było coś niesamowitego. Szkoda, że konkurs już się skończył. Ale zostawił na pewno w nas bardzo miłe wspomnienia, czekamy na kontynuację! :) 

Ale nie zbaczajmy z tematu, to jeszcze nie czas na podsumowanie. Głównymi beneficjentami konkursu są oczywiści poszczególni użytkownicy, którzy wygrali nagrody. Ale również sam vortal dobreprogramy.pl no i oczywiście... INTEL. Reklamę jaką sobie zrobiła firma Intel jest wręcz bezcenna. Przez miesiąc logo była na stronie głównej dp.pl, każda z osób biorących udział w konkursie czekała na pytania związane z firmą Intel, świadomość związana z marką wzrosła niewątpliwe. 
Przeliczmy wartość nagród (ceny z ceneo.pl, cena plecaka obliczona &quot;na oko&quot;:P):

         1x   MSI Classic CR620-049XPL -  1x 2 145zł = 2 145zł
         3x   ASUS Eee PC 1001PX -          3x 1 059zł = 3 177zł
         30x Plecak intel -                        30x   150zł  = 4 500zł 
--------------------------------------------------------------------
                                                                                9 822 zł

Nie jestem tam jakimś marketingowcem, ale nie jest to chyba wygórowana wartość jak na miesięczny konkurs. Oczywiście pewnie firma Intel mogła dopłacić dla osób przygotowujących konkurs i &quot;wesprzeć&quot; dobreprogramy.pl Ale chyba popularność konkursu zaskoczyła wszystkich i przyniosła dla każdej ze stron wymierne korzyści. 

Uffff, zaraz, miało być o wykrywaniu diody, a nie jakieś analizy konkursu:) Zatem do dzieła.





## Dioda konkursowa od kuchni



Opisany sposób jest jedynie informacja, o tym jak można było wykryć diodę jednym z wielu, wielu sposobów. 

Pierwsze spojrzenie na diodę mogło mylnie sugerować, iż żółta dioda zapala się poprzez plik swf: 

[http://www.dobreprogramy.pl/App_Themes/Intel/images/dioda.swf](http://www.dobreprogramy.pl/App_Themes/Intel/images/dioda.swf)

Jednakże już samo spojrzenie na sam plik swf, sugerowało, iż jest inaczej. Gdy pytanie konkursowe było aktywne, żółta dioda konkursowa była ustawiana jako tło i &quot;przykrywana&quot; plikiem swf który przyjmował kolor niebieski, lub był przezroczysty, co sprawiało, iż dioda migała na żółto. Ktoś w komentarzach, słusznie zauważył, iż dioda na stronie [http://konkurs.dobreprogramy.pl/](http://konkurs.dobreprogramy.pl/), gdy nie ma pytania miga na niebiesko. Oczywiście. Tło było niebieskie, a plik swf z niebieskim kolorem migał również niebieskim kolorem.

Następnie należało odkryć skąd jest brany kolor diody. Z pomocą przyszedł dodatek Firebug do Firefoxa, po jego uruchomieniu otrzymałem coś niezwykle pomocnego:



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-11-2-_194_/g_-_608x405_-_-_21254x20101030155748_1.png

 *Rys. 1 Dioda w ostatnim dniu konkursu* 

Na załączonym obrazu widać, iż tło z diodą pobierane jest z web serwisu. Musimy zatem pobrać te tło i odpowiednio je zinterpretować, aby móc wykryć żółtą diodę.

Zdjęcie pochodzi z ostatniego dnia konkursowego. 



## Dioda miała kilka wcieleń podczas całego konkursu. Postaram się opisać każde z nich oraz sposób wykrycia żółtej diody. 





Przepis na diodę - Dioda w sosie własnym

Załóżmy, że korzystamy z darmowych, dostępnych składników. Oto one:

Do wykrycia diody potrzebujemy:
- instalka Microsoft Visual C# 2010 Express
- Firefox
- dodatek Firebug do Firefoxa
- połączenie z internetem

Czas przyrządzenia wersji najprostszej: kilka minut.

Smacznego! 





## I jeszcze coś...



Po przeanalizowaniu regulaminu konkursu, nie znalazłem nic, co mówiło by o tym, iż nie można używać aplikacji do sprawdzania diody. Dodatkowo wiele osób w  komentarzach pod wpisami na stronie głównej chwaliło się swoimi programami. A, że czołówka w większość miała aplikacje jakieś własne, to chyba nikt w to nie wątpi. 





## Dioda 1.x



 */Analiza - Dioda 1.0/* 
Pierwsza dioda była bardzo prosta:

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-11-2-_194_/g_-_608x405_-_-_21254x20101030165340_2.png

 *Rys. 2 Dioda 1.x zwracana przez web serwis*  

Zabezpieczaniem był prostokąt zawierający losowe kolory pikseli. Co uniemożliwiało sprawdzenie, czy web serwis zwraca diodę żółtą, na podstawie rozmiaru/sumy kontrolnej obrazka. 

Link do web serwisu był również ciekawy:

 *http://www.dobreprogramy.pl/ContesstIsActive.ashx?q=20101009124534* 

Query string zawierał ciąg znaków, który był &quot;losowy&quot;. Dzięki czemu na starszych przeglądarkach (np. IE6) obrazek zwracany z web serwisu nie był cacheowany.
Jednakże łatwo zauważamy, iż jest to aktualna data w formacie: 

 *ROKmiesiącDZIEŃgodzinaMINUTAsekunda* .


 */Kod - Dioda 1.0/* 

Zastosowałem Obiekt Parametrs, dzięki czemu niektóre parametry można było ustawić w oknie opcji.
Opis parametrów obiektu Parameters:

```csharp

par.Ur - url do web serwisu, który zwracał obrazek z diodą

par.PixelX - współrzędna X jaką należy sprawdzić
par.PixelY - współrzędna Y jaką należy sprawdzić

par.ColorR_From - składowa R pixela, granica dolna
par.ColorR_To - składowa R pixela, granica górna

par.ColorG_From - składowa G pixela, granica dolna
par.ColorG_To - składowa G pixela, granica górna

par.ColorB_From - składowa B pixela, granica dolna
par.ColorB_To - składowa B pixela, granica górna

```
 

Kod sprawdzający czy dioda się &quot;zapaliła&quot;:

```csharp

public bool IsDiodeActive(Parametrs par)
{

DateTime now = DateTime.Now;


                    WebClient wc = new WebClient();
                    byte
```
 data = wc.DownloadData(par.Url
                        + &quot;?q=&quot;
                        + now.Year.ToString(&quot;0000&quot;)
                        + now.Month.ToString(&quot;00&quot;)
                        + now.Day.ToString(&quot;00&quot;)
                        + now.Hour.ToString(&quot;00&quot;)
                        + now.Minute.ToString(&quot;00&quot;)
                        + now.Second.ToString(&quot;00&quot;)
                        );

                    Bitmap bitmap = new Bitmap(new MemoryStream(data));

                    Color c = bitmap.GetPixel(par.PixelX, par.PixelY);

                    if (c.R &gt;= par.ColorR_From &amp;&amp; c.R = par.ColorG_From &amp;&amp; c.G = par.ColorB_From &amp;&amp; c.B = par.ColorR_From &amp;&amp; c.R = par.ColorG_From &amp;&amp; c.G = par.ColorB_From &amp;&amp; c.B &lt;= par.ColorB_To)
                    {
                        return true;
                    }
                    else
                    {
                        return false;
                    }
}

[/code]

Krótki opis:
- metoda IsDiodeActive zwraca true/false z informacją czy dioda się zapaliła, czy nie
- za pomocą obiektu WebClient pobieramy obrazek z web serwisu
- tworzymy link z uwzględnieniem query stringa (nie jest to obowiązkowe!)
- rzutujemy pobrane dane na bitmapę
- wyciągamy odpowiedni pixel z bitmapy
- sprawdzamy czy RGB pixela mieści się w granicach dla żółtej diody

 *Update - Dioda 1.1* 
W międzyczasie, było kilak zmian, które sprowadzały się do zmiany nazwy web serwisu zwracającego dane. Trudność polegała na tym, iż stary web serwis zostawał aktywny, lecz zwracał cały czas niebieską diodę. Dzięki temu, iż url do web serwisu był w parametrach, można było szybko podmienić poprawny web serwis.

Podsumowanie
+ świetny pomysł z samą diodą i plikiem swf
- trochę słabe zabezpieczenia

Ogólna ocena:
4-/6






## Dioda 2.x



 */Analiza - Dioda 2.0/* 

Kolejne wcielenie diody było miłym zaskoczeniem. Ktoś tam po drugiej stronie włożył w to sporo pracy. Nazwałem tą wersje 2.0, gdyż zmiany są dość znaczące: (kliknij by powiększyć!)

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-11-2-_194_/g_-_608x405_-_-_21254x20101030165525_3.png

 *Rys. 3 Dioda 2.x*   

Jak zwykle z pomocą przyszedł Firebug. Z załączonego obrazka widzimy, iż bitmapa zwracana przez web serwis, już jest inna. Znajdują się na niej 8 diod. Nawet gdy nie było pytania, zawierała ona zarówno niebieskie, jak i żółte diody. Celem było znalezienie w jaki sposób wybierana jest dioda poprawna, do wyświetlenia. 

Tak, Firebug jest niemalże niezbędny:P Szybka analiza kodu strony, pozwoliła na znalezienie ukrytego kodu CSS, który odpowiadał za przesuniecie bitmapy tak, by odpowiednia dioda została wyświetlona, patrz rys. 3 (A).

 */Kod- Dioda 2.0/* 

Zmieniony kod:

```csharp
public bool IsDiodeActive(Parametrs par)
{
WebClient wc = new WebClient();
                    byte
```
 dataHtml = wc.DownloadData(&quot;http://konkurs.dobreprogramy.pl/&quot;);
                    string plainHtml = Encoding.UTF8.GetString(dataHtml);

                    Point p = GetOffset(plainHtml);

                    byte[] dataImg = wc.DownloadData(&quot;http://konkurs.dobreprogramy.pl/ContestHandler.ashx?q=&quot; + GetQuery(plainHtml));

                    Bitmap bitmap = new Bitmap(new MemoryStream(dataImg));
                    Color c = bitmap.GetPixel(par.PixelX + p.X, par.PixelY + p.Y);

(... dalej jak w wersji 1.0 )
}
[/code]

Krótki opis:
- zmiana była dość znacząca, teraz pobieramy cała stronę (http://konkurs.dobreprogramy.pl/, gdyż jest lżejsza niż http://dobreprogramy.pl)
- dla strony metoda GetQuery odszukuje query string do doklejenia na koniec zapytania do web serwisu (także nie jest to obowiązkowe!)
- metoda GetOffset dla pobranej całej strony wyszukuje przesunięcie, algorytm jest maxymalnie prosty, wyszukujemy słowa #diode, i tniemy/skracamy kod aż będziemy mieli pożądane dane (patrz rys. 3 (A))
- teraz ściągamy bitmapę z ośmioma diodami
- robimy przesunięcie pixela o dane otrzymane z parsowania strony html przez metodę GetOffset
- dalej robimy taka samo jak dla diody 1.x


 *Update - Dioda 2.5* 
Bardzo znaczący update diody. Można powiedzieć, iż wersja 2.0 powinna od razu zawierać zmiany wprowadzone w wersji 2.5.

W samej diodzie nic się nie zmieniło. Zmienił się tylko (lub aż), kod CSS ustawiający diodę. Prosty kod CSS (patrz rys. 3 (A)), został zamieniony na &quot;zamotany&quot; kod przedstawiony na rys. 3 (B).

Jednakże przyklejając go do Notepad++ szybko się orientujemy, że kod ten został tylko delikatnie obfuskowany, co widzimy na rys. 3 (C). Dodano komentarze, które zaciemniały kod. Mała zmian, ale dość pomysłowa :)

Zatem należało zmienić tak algorytm, ażeby najpierw usunął komentarze z kodu CSS. Dodatkowo w tej wersji url do web serwisu, brać można również z kodu CSS, co zostało zaznaczone na (B) i (C).

 */Kod- Dioda 2.5/* 

Zmieniony kod:

```csharp
public bool IsDiodeActive(Parametrs par)
{
WebClient wc = new WebClient();
                    byte
```
 dataHtml = wc.DownloadData(&quot;http://konkurs.dobreprogramy.pl/&quot;);
                    string plainHtml = Encoding.UTF8.GetString(dataHtml);

                    string[] values = GetDataFromHtml(plainHtml);
                    Point p = new Point(int.Parse(values[1]), int.Parse(values[2]));

                    byte[] dataImg = wc.DownloadData(&quot;http://konkurs.dobreprogramy.pl&quot; + values[0]);

                    Bitmap bitmap = new Bitmap(new MemoryStream(dataImg));

                    Color c = bitmap.GetPixel(par.PixelX + p.X % 108, par.PixelY + p.Y % 108);

(... dalej jak w wersji 2.0 )
}
[/code]

Krótki opis:
- nadal pobieramy kod html z http://konkurs.dobreprogramy.pl/
- parsujemy go metodą GetDataFromHtml, która z zaznaczonego kodu (B) pobiera adres do web serwisu oraz przesunięcie. Oczywiście wcześniej pozbywa się komentarzy w kodzie CSS
- gdy już mamy uri do web serwisu i przesunięcie, ściągamy obrazek z diodami
- na tym etapie musimy jeszcze, na owym znalezionym przesunięciu zastosować działanie modulo 108, gdyż wartością mogą być większe niż rozmiar obrazka (108 px)
- następnie robimy jak w poprzednich aplikacjach, czyli sprawdzamy kolor pixela

 *Update - Dioda 2.6* 
Taaak, to było genialne. W piątek, czyli w ostatnim dniu, kiedy było pytanie normalne, zmieniono obliczanie przesunięcia:) Było to o tyle genialne, iż nikt nie spodziewał się, że przed ostatnim pytaniem normalnym, redakcji będzie chciało się cokolwiek  zmieniać :P Za to duży plus :)
 
Podsumowanie
+ sporo zmian w stosunku do wersji 1.x
+ ciekawy pomysł z przesunięciem w kodzie CSS
+ dopiero teraz zaczęło coś się dziać :P

Ogólna ocena:
5+/6






## Podsumowanie




Mam nadzieje, że przedstawione sposoby zachęcą kogoś do zagłębienia się w programowanie. Przedstawione kody źródłowe były dość ogólne. Sposób wyświetlania diody już się zmienił (wersji 2.6 jeszcze nie zrobiłem:P).

Oczywiście, może ktoś napisać, iż prostszym sposobem i efektywniejszym było sprawdzanie koloru diody w już wygenerowanej stronie za pomocą jakiegoś color pickera. I miałby rację! Ale, takie pisanie programu, który analizuje stronę html, web serwis itp., dostarczało mi większej radości. A o to tu chyba chodziło :)

Może napiszę jeszcze co mi się nie podobało w konkursie. Przede wszystkim pytania w nocy! Pytania o 7 z rana są jeszcze w ok, ale o 2 w nocy to już lekka przesada. Również pytania specjalne ze względu na ich wyższy stopień zaawansowania, można było oceniać wg innej (wyższej) punktacji. Poza tym dla 2. i 3. miejsca można było jakieś małe nagrody dać. Chociaż po plecaku :P 

Mając możliwość, dziękuje redakcji, iż mogłem wziąć udział w tak emocjonującym i dającym wiele frajdy konkursie. Coś niesamowitego! Dzięki. Gratuluje zwycięzcom i wszystkim uczestnikom konkursu! Mam nadzieję, iż jeszcze zostanie zorganizowany jakiś podobny konkurs, gdyż takiej pozytywnej energii zgromadzonych we wszystkich uczestnikach konkursu, nie można zmarnować!:)

No i pozdrowienia dla dwóch osób z teamu ;)

Dziękuję i pozdrawiam.)