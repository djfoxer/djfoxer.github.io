---
layout:     post
title:      UrlRewritingNet.UrlRewrite na nowych wersjach IIS
date:       2013-01-30 15:41:00
summary:    Wszytko idzie do przodu. Nowe wersje Windows Server, kolejne wydania IIS, co chwila udoskonalany framework .NET... świat IT leci do przodu jak oszalały. Kolejne reklamy promujące śweżynki, czy to w postaci oprogramowania lub sprzętu. Każdy musi mieć najnowszą wersję, najbardziej wypasiony sprzęt. Ni...
categories: <input id="chkTagsList_3" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_3" checked="checked" value="8"><label for="chkTagsList_3">oprogramowanie</label> <input id="chkTagsList_6" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_6" checked="checked" value="64"><label for="chkTagsList_6">porady</label> <input id="chkTagsList_10" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_10" checked="checked" value="1024"><label for="chkTagsList_10">serwery</label>
---



Wszytko idzie do przodu. Nowe wersje Windows Server, kolejne wydania IIS, co chwila udoskonalany framework .NET... świat IT leci do przodu jak oszalały. Kolejne reklamy promujące śweżynki, czy to w postaci oprogramowania lub sprzętu. Każdy musi mieć najnowszą wersję, najbardziej wypasiony sprzęt. Niestety w szarej rzeczywistości IT nieraz jesteśmy zmuszani do tego, aby działać ze starszym oprogramowaniem. Często dawno napisane aplikacje już nie sposób jest przepisać na nowy framework. Powody mogą być różne. Użycie zewnętrznych bibliotek, które już nie są wspierane, współpraca z innym starszym oprogramowaniem, zastosowanie składni/poleceń, które już zostały usunięte w nowych wersjach frameworka, czy po prostu brak czasu/zasobów na przeniesienie kodu do nowej wersji i ponowne testy.



Mam kontakt z oprogramowaniem, które również nie można przenieść na nowe wersje frameworku ze względu na kilka mniejszych i większych zależności, które wymieniłem. Nie ma już to większego znaczenia. W czym jednak jest problem? Otóż pewien projekt w czystym ASP.NET 3.5 (w sumie to 2.0) korzysta z biblioteki [UrlRewritingNet.UrlRewrite](http://www.urlrewriting.net) (nie jest ważne dlaczego ktoś to użył i nie ma możliwości zmiany, zapewne wielu z Was ma również styczność z tego typu projektami). Jest to projekt, który pozwala na starszych wersjach ASP.NET korzystać z tzw. przyjaznych linków np. zamiast
 *adres/Details.aspx?id=123&param=abc*  
można użyć: 
adres/Produkt/123/abc. 
Często używany przez SEO itp. Niestety, nie można go już w realnym czasie przepisać na MVC, czy coś podobnego. Użycie [UrlRewritingNet.UrlRewrite](http://www.urlrewriting.net) sprawiło, że wystawiając go na serwerze z nowym IIS, trzeba się pomęczyć, aby wszystko działało jak należy. 

Przestawię mały poradnik jak zmusić  [UrlRewritingNet.UrlRewrite](http://www.urlrewriting.net) do działania na nowym IIS. Oto wymagane kroki:





  * przechodzimy na witrynę w  *IIS Manager*  na jakiej chcemy zmienić ustawienia


  * przechodzimy do  *Mapowania obsługi* 


  * edytujemy wpis  *StaticFile* 




  * zmieniamy w nim  *Ścieżkę żądania*  na :*.*


  * otwieramy  *Ograniczenie żądań*  i na zakładce  *Mapowanie*  zaznaczamy 
  * Plik



  *  zatwierdzamy podwójnie wybór









  * będąc w opcjach  *Mapowania obsługi*  dodajemy (menu po prawej) mapę skryptu




  *  *ścieżka żądania* : *


  *   *wykonywalny* : %windir%\Microsoft.NET\Framework\v2.0.50727\aspnet_isapi.dll


  * nazwa: Wildcard


  * otwieramy  *ograniczenie żądań*  i na zakładce  *Mapowanie*  odznaczamy checkboxa " *Wywołaj obsługę tylko, jeśli....* "


  * zatwierdzamy podwójnie, na pytanie o ISAPI odpowiadamy twierdząco











  * będąc w opcjach  *Mapowania obsługi*  dodajemy (menu po prawej)  *mapę skryptu* 



  *  *ścieżka żądania* : *.html


  *  *wykonywalny* : %windir%\Microsoft.NET\Framework\v2.0.50727\aspnet_isapi.dll


  *  *nazwa* : HTML VIRTUAL


  * otwieramy  *ograniczenie zadań*  i na zakładce  *Mapowanie*  odznaczamy checkboxa  *Wywołaj obsługę tylko, jeśli....* 


  * w tym samym oknie na zakładce  *Zlecenia*  zaznaczmy  *Jedno z następujących zleceń*  i wpisujemy:  *GET,HEAD,POST,DEBUG* 


  * zatwierdzamy podwójnie, na pytanie o ISAPI odpowiadamy twierdząco











  * będąc w opcjach  *Mapowania obsługi*  zaznaczmy (w menu po prawej) opcję  *Wyświetl listę uporządkowaną* 




  * za pomocą opcji  *Przenieś w dól/górę*  przenosimy  *Wildcard*  tak, aby znajdował się pod  *StaticFile* 


  * przenosimy  *HTML VIRTUAL*  tak, aby znajdował się pod  *ASPClassic* 


  * 










  * w drzewku po lewej zaznaczamy naszą witrynę i w menu po prawej zaznaczamy  *Ustawienia zaawansowane* 



  * w opcji  *Pula aplikacji*  wybieramy  *Classic .NET AppPool* 











Od tej pory dana aplikacja z [UrlRewritingNet.UrlRewrite](http://www.urlrewriting.net) powinna bez problemów chodzić na nowych wersjach IIS. Jestem świadom, iż powyższa metoda ma zarówno  plusy, jak i minusy. Jednakże całość funkcjonuje świetnie i nie ma problemów z działaniem. Mam nadzieję, że wpis będzie pomocny w rozwiązywaniu tego typu problemów lub podobnych.