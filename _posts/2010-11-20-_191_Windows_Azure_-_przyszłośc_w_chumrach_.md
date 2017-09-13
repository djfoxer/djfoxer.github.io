---
layout:     post
title:      Windows Azure - przyszłośc w chumrach?
date:       2010-11-20 18:43:00
summary:    Rewolucja czy ewolucja?Windows Azure - usługa (system) do przechowywania danych w chmurze oraz udostępniania infrastruktury, za ustaloną cenę. Premiera Azura w Polsce miała miejsce jakiś czas temu. Jest to ciekawa technologia, oparta na chmurze, przedstawiona przez Microsoft. Rys 1. Diagram platform...
categories: sprzęt programowanie serwery
---



Rewolucja czy ewolucja?

Windows Azure - usługa (system) do przechowywania danych w chmurze oraz udostępniania infrastruktury, za ustaloną cenę. Premiera Azura w Polsce miała miejsce jakiś czas temu. Jest to ciekawa technologia, oparta na chmurze, przedstawiona przez Microsoft.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-11-20-_191_/g_-_608x405_-_-_21587x20101120155952_1.jpg)

 
 *Rys 1. Diagram platformy Azure * 

Ogólnie patrząc, Azure oferuje nam: zestaw usług dostępnych w chmurze, infrastrukturę do hostowania aplikacji i narzędzia do zarządzanie nim. 

Mówią nam, że pomysł nie jest nowy. Przykładem niech będzie prąd. Płacimy za możliwość odbioru prądu. Czyli za usługę. Twórcą modelu był Tesla, który sprzedawał prąd. Ten model się przyjął. Zaś zupełną porażką zakończył się pomysł Edisona, ażeby sprzedawać nie prąd (usługę), lecz generatory i wynajmować specjalistów od nich. Czy podobnie będzie w środowisku usługodawców hostingowych? Obecnie nie jest łatwo odpowiedzieć na to pytanie. Zauważmy, iż Microsoft udostępnia również tą technologię, do budowy własnych chmur Azure. Chmura jest zbiorem tzw. Data Center (dalej DC), które są rozsiane po całym świecie. Możemy zarówno korzystać z usług DC przygotowanych przez Microsoft, jak i kupić / wypożyczyć DC od Microsoftu. Wówczas będziemy posiadaczami własnej chmury Azure.
 




## Szczegóły Microsoft Azure




System Azura składa się z kilku składników:
- Azure Storage - są to takie elementy jak: Kolejki (tzw. ticket w kolejce może mieć max. 8KB), Bloby (dane niestrukturalne, można w uogólnieniu porównać do trywialnego  FTP), Tabele Azure (specjalne tabele służące jako składowe danych, posiadają swój unikalny klucz, ale nie mogą mieć kluczy obcych, dane strukturalne, do max. 1 MB w wierszu)
- Azure Drive - Blob sformatowany jako NTFS
- SQL Azure - specjalna baza SQL dla Azure
- CDN - sieć DC przechowująca dane w Blobach, będących w najmniejszej odległości od klienta
- Role - usługi działające w chmurach, logika aplikacji
- AppFabric - kontrola dostępu, kanał informacyjny
- API zarządcze - API do zarządzania, monitorowania usług, ról działających w naszej chmurze Azure

Pojedyncza, najmniejsza wirtualna komórka DC Azura to: 
CPU: 1.6 GHz x64
Pamięć: 1.6GB 
Sieć: 100Mbps
Storage: 250GB

Posiada ona zainstalowane:
- Windows Server Enterprise 2008
- IIS 7.0
- .NET 3.5 SP1 / 4.0
- dodatkowa możliwość uruchomienia aplikacji napisanych w: Java, PHP, Python, Ruby
- system Azure OS (tzw. &quot;Guest&quot;), w różnych wersjach, dzięki czemu możemy uruchamiać usługi zoptymalizowane/napisane dla różnych wersji Azuer OSa

Możemy zaprzęgnąć do nasz pracy, następujące maszyny VM Azura:

Bardzo mała 
CPU: 1 GHz 
Pamięć : 768 MB 	
Storage: 20 GB 
	
Mała 
CPU: 1,6 GHz 
Pamięć: 1,75 GB 
Storage: 225 GB 
	
Średnia 	
CPU: 2 x 1,6 GHz 
Pamięć: 3,5 GB 
Storage: 490 GB
 	
Duża 
CPU: 4 x 1,6 GHz
Pamięć: 7 GB 
Storage: 1000 GB 	

Bardzo duża 	
CPU: 8 x 1,6 GHz 	
Pamięć: 14 GB 	
Storage: 2040 GB 	



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-11-20-_191_/g_-_608x405_-_-_21587x20101120163825_2.jpg)

 
 *Rys 2. Jedno z setek, rozsianych po świecie, Data Center Azura (na zdjęciu w San Antonio) * 






## Cena




Za te przywileje Microsoft, każe sobie płacić. I to nie mało. W Linku [2] można obejrzeć za co musimy i ile zapłacić (chmura na serwerach Microsoftu, nie własnych).
Ceny domyślnych stawek w Azure:

Instancja obliczeniowa
- Mała instancja (domyślnie): 0,0852 € za godzinę
Magazyn
- 0,1064 € za GB zapisywany miesięcznie
- 0,0071 € za 10 000 transakcji zapisywania
Obsługa CDN
- 0,1064 € za 1 GB transferu danych 
- 0,0071 € za 10 000 transakcji 
SQL Azure
- 7,085 € za bazę danych do 1 GB miesięcznie


Oczywiście nie są to wszystkie opłaty, polecam zajrzeć do linku [2] ze stawkami obowiązującymi w Azure. 

Przeglądając te dane dojdziemy do wniosku, iż nie są to ceny atrakcyjne. Usługi udostępniane przez Amazon i Google są w pewnych wariantach tańsze. Dodatkowo warto zaznaczyć, iż opłata pobierana jest za wgranie usługi. Nie ma znaczenia, czy usługa działa, czy nie. Czy zawiesiła się (a propos zawieszenia się usługi, Azure po tym, jak jakaś usługa się zawiesi, sam ją restartuje!), czy nawet nie zdążyła się uruchomić. W każdym z tych przypadków pobrane zostaną opłaty wg cennika!




## Jak rozpocząć przygodę z Azure?



Aby móc rozpocząć pracę z Azure należy zarejestrować się na Microsoft Online Services [5] (Rysunek 3.). Niezbędne jest posiadanie Windows Live Id! Na stronie [5] aktywujemy podstawowy pakiet Azure. Rejestracja jest długa i mało intuicyjna. Musimy posiadać kartę kredytową już na etapie rejestracji! 




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-11-20-_191_/g_-_608x405_-_-_21587x20101120175757_3.png)

 
 *(Kliknij aby powiększyć)
Rys 3. Konto na Microsoft Online Services [4] 
Rys 4. Założony podstawowy Storage w Windows Azure
Rys 5. Szczegóły usługi w Windows Azure* 

Jeśli przebrniemy przez kilkanaście (sic!) ekranów rejestracji, powita nas piękna strona Windows Azure.  Wówczas możemy zacząć tworzyć własne magazyny (usługi) w chmurze, i przerzucać do nich dane (Rysunek 4.). A także pobudzać do życia usługi Azure (Rysunek 5.).

Od strony programisty przygotowano Toolkit Azura dla Visual Studio 2010. Wymagane środowisko to Windows Vista z Sp1/Server 2008/7 z IIS 7.0 (+). Postaram się umieścić w przyszłości, krótki programik z wykorzystaniem Azura, uruchomionego lokalnie. 




## Dlaczego Azure?



Azure, a w sumie i ogólna postać chmury, daje nam niewątpliwie wiele zalet:
- koszty infrastruktury są niezmienne
- brak problemów związanych z działaniem sprzętu hostingowego (awarie, chłodzenie, koszty administracyjne)
- &quot;nieograniczona&quot; moc obliczeniowa
- działania zabezpieczające po stronie Azure
- automatyczne i dynamiczne dopasowanie infrastruktury do obciążeń
- dostępność na poziomie 99,99%
- CDN automatycznie dopasowujący się do położenia klienta (aby osiągnąć jak największą szybkość klient &lt;-&gt; serwer)
- gwarancja firmowana przez Microsoft

Azure &quot;śmierdzi&quot;?


Sama technologia Azure jest bardzo ciekawa i ma wiele zalet, jednak już przy pierwszy zetknięciu napotkamy na kilka rzeczy, które mogą wywoływać grymas na twarzy:
- sama technologia chmury jest zupełnie innym podejściem do &quot;hostingu&quot;, może to powodować opory, szczególnie &quot;u góry&quot;
- koszty Azure nie są konkurencyjne w stosunku do Amazona, Google
- brak jakiegokolwiek środowiska testowego w chmurze! Mając środowisko testowe-lokalne na komputerze (np. Visual Studio z Toolkitem do Azura), otrzymujemy 95% zgodności z realną chmurą Azure. Mozna było by np. stworzyć chmurę do testów, która miała by ograniczenia na CPU, pamięć, storage. Ewentualnie, w chmurze testowej, dane były by czyszczone co pewien czas. 
- uciążliwa rejestracja do Azura
- opłata już na etapie wgrania aplikacji do chmury






## Słowem podsumowania




Microsoft Azure i ogólnie sama idea chmury są zapewne przyszłością. Azure ma wiele zalet, jednakże obawiam się czy w natłoku innych, już dostępnych dłużej, środowisk, nie zostanie ona zmarginalizowana. Mam nadzieje, że to nie nastąpi. A Microsoft rzuci na rynek bardziej &quot;ludzkie&quot; ceny dla Azure. Liczę na to :) 


Dodatkowo zachęcam do zapisania się na szkolenia z Azura w &quot;Akademii Azura&quot; [4]!

Dziękuję i pozdrawiam.  

Linki:
[1][Microsoft Azure Homepage](http://www.microsoft.com/windowsazure/)
[2][Cennik usług Azure](http://www.microsoft.com/windowsazure/offers/popup/popup.aspx?lang=pl&amp;locale=pl-PL&amp;offer=MS-AZR-0003P) 
[3][Film przedstawiający koncepcję Data Center](http://www.youtube.com/watch?v=PPnoKb9fTkA)
[4][Akademia Azura](http://www.microsoft.com/poland/aa/default.aspx)
[5][Microsoft Online Services - centrum, gdzie zakupujemy i zarządzamy usługami m.in. Azure](https://mocp.microsoftonline.com/site/default.aspx?uiculture=pl)
