---layout:     post
title:      Kafelki w serwerze - piąte koło u wozu?
date:       2012-12-10 14:16:00
summary:    O kafelkach, czyli nowym interfejsie Modern w najświeższych Okienkach, napisano już tyle, że aż można dostać niestrawności, czytając w kółko to samo. Ten wpis będzie jednak zupełnie inny. Otóż przedstawię kilka faktów technicznych związanych z nimi, a także jak wyglądają i jak mogłyby wyglądać na ma...
categories: windows oprogramowanie serwery
---



O kafelkach, czyli nowym interfejsie Modern w najświeższych Okienkach, napisano już tyle, że aż można dostać niestrawności, czytając w kółko to samo. Ten wpis będzie jednak zupełnie inny. Otóż przedstawię kilka faktów technicznych związanych z nimi, a także jak wyglądają i jak mogłyby wyglądać na maszynie serwerowej. 



### Mobilnie



Aplikacje w Modern UI na Windows Server 2012 działają na podobnej zasadzie co te w wersji desktopowej, na tabletach, czy smartfonach. Zamysł jest ciekawy - ujednolicenie kilku środowisk graficznych, dzięki czemu przejście pomiędzy nimi, jest płynne i bezproblemowe. W drodze do domu przeglądamy pocztę na Windows Phone, czy tablecie z Windows 8 RT. Zaś w mieszkaniu uruchamiamy stacjonarny komputer i kontynuujemy czytanie wiadomości na stacjonarnym Windows 8. Wszędzie interfejs kafelkowy jest ten sam i działa w podobny sposób. To idealne GUI pod ekrany dotykowe. Obsługa w Windows Phone, czy tabletach na nowych okienkach jest przyjemna, prosta i intuicyjna. Podobnie jest w przypadku notebooków i im pochodnych, które posiadają dotykowy ekran (których powoli jest coraz więcej). 



### Stacjonarnie



Na desktopie jest już jednak trochę inaczej. Ekrany dotykowe w domu to jeszcze nie codzienność, przynajmniej u nas. Nie tylko ze względu na cenę, ale również na to, iż obsługa palcem przez dłuższy czas jest bardzo męcząca.  Jednakże i w tym przypadku Modern UI jest takie jak na urządzeniach przenośnych. Posiada również te same zalet i wady, przy czym  te ostatnie mogą być jeszcze bardziej widoczne. Pamiętać należy, iż w większości przypadków, komputer w domu to klasyczna jednostka stacjonarna lub tzw. &quot;komputer do salonu&quot;. W obu przypadkach dotykowy ekran może sprawdzić się świetnie dla użytkowników chcących szybko odebrać pocztę, przeczytać news z ulubionego portalu, czy przejrzeć RSSy. Nadal jednak mowa jest o krótkim, niezobowiązującym przebywaniu z wersją dotykową systemu. Pomysł, aby interfejs ModernUI był wszędzie identyczny jest ciekawy. Trochę jednak zbyt mocno trzymano się ujednolicania wszystkiego. W większości przypadków komputery desktopowe podłączone są do sieci, a zatem nie ma sensu sztuczne oszczędzanie prądu. W ModernUI w tym przypadku ma jednak ograniczenia, jak w wersji na urządzenia mobile m.in. usypianie procesów działających w tle, czy wybudzanie aplikacji w tle co 15 minut (nie częściej). Pomimo powiadomień  *push* , nadal nie wszystko można zrobić gładko i przyjemnie, jak chociażby komunikator, czy kafelek będący zegarkiem. Ograniczenia nałożone na desktopie są  co najmniej dziwne.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-10-_114_/g_-_608x405_-_-_37780x20121209141122_0.png






### Serwerowo - jak jest, a jak mogło być



Czas teraz na Windows Server 2012. Otóż Microsoft idąc za ciosem, wprowadził interfejs ModernUI w serwerową wersję okienek. Nie różni się on niczym od tego znanego z Windows 8. Po czystej instalacji, w kafelkowym menu otrzymujemy tylko kilka skrótów i nic więcej. Co ciekawe. Domyślnie nie można nic instalować z Windows Store, gdyż ta funkcjonalność nie jest zainstalowana. Możną ją szybko dodać (opisał to [B.Andy](http://www.dobreprogramy.pl/B.Andy/Howto-Windows-Server-Workstation,37579.html)), ale świadczy to tylko o tym jak bardzo może być ona &quot;użyteczna&quot; na maszynie serwerowej. Skoro sami twórcy, wyłączyli tą rolę, w takim razie jaki jest sens istnienia kafelków w Windows Server? 

)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-10-_114_/g_-_608x405_-_-_37780x20121209143215_0.png



Pewnie jak to ostatnio bywa, z tym wszystkim co ma w nazwie Windows 8, nie było czasu na dopieszczenie całości. A Microsoft mógł dodać kilka kafelków skierowanych tylko do maszyn serwerowych. W pracy mam styczność głównie z IIS i bazą danych na Windows Server. Myślę, że niegłupim pomysłem byłoby aby np. stworzono kafelki właśnie dla tych &quot;modułów&quot;. Szybki podgląd na stan jakiejś wybranej aplikacji na IIS, czy stan bazy. Ciekawie mogłoby wyglądać także eventlog na kafelku! Wystarczyłoby wprowadzić filtr i kafelek pokazywałby ostatnie zdarzenia z ich liczbą na stronie ModernUI. Po zalogowaniu do serwera, każdy szybko by sprawdził najważniejsze wiadomości o wybranych zdarzeniach, czy usługach, jedynie wciskając klawisz  *Windows* .


)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2012-12-10-_114_/g_-_608x405_-_-_37780x20121209153629_0.png



Powyżej zamieściłem zrobiony szybko taki przykładowy kafelek. Widzimy w nim jakieś eventy, które pokazują się na podstawie wybranego wcześniej filtru. Oczywiście tylko kilka ostatnich. Dodatkowo, w dolnym prawym rogu, wyświetla się ilość wszystkich powiadomień. Duża ikona symbolizuje typ zdarzeń (błędy, informacje, itp.). Do ekranu startowego można przyczepić kilka takich kafelków, o różnych filtrach i dla różnych zdarzeń. Myślę, że to mógłby być całkiem ciekawy pomysł. Mógłby być, ale nie jest. Dlaczego? Otóż zwykły programista piszący na ModernUI,  nie ma dostępu do danych na dysku. Jedyna szansa to firmy współpracujące z  MS. Myślicie, że to niemożliwe? Wystarczy przejrzeć aplikacje Noki na Windows Phone. Część z nich to nie tylko zwykłe aplikacje, ale rozszerzenia Windows Phone, głęboko integrujące się w system (jak chociażby Licznik). 

Kafelki w Windows Server 2012 to ciekawy pomysł, ale trochę niewykorzystany. W obecnej formie jest to raczej zbędny gadżet, może jednak coś się zmieni razem z rozwojem systemu i wypuszczaniu kolejnych aktualizacji. )