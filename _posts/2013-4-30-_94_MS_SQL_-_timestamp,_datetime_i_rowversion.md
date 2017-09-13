---
layout:     post
title:      MS SQL - timestamp, datetime i rowversion
date:       2013-04-30 17:56:00
summary:    Tworząc bazę często natykamy się na konieczność stworzenia mechanizmu, który będzie pozwalał na wykrywanie zmian w poszczególnych wierszach tabeli. Różne są podejścia do tego zagadnienia. Na przykładzie bazy MS SQL można rozwiązać to na kilka sposobów. Do tego celu idealnie nada się change tracking ...
categories: porady programowanie
---



Tworząc bazę często natykamy się na konieczność stworzenia mechanizmu, który będzie pozwalał na wykrywanie zmian w poszczególnych wierszach tabeli. Różne są podejścia do tego zagadnienia. Na przykładzie bazy MS SQL można rozwiązać to na kilka sposobów. Do tego celu idealnie nada się change tracking z tombstonem, czy CDC (change data capture) dla wersji enterprise. W tym wpisie skupię się jednak na prostszym rozwiązaniu, a mianowicie timestampie, który jest realizowany automatycznie (wystarczy kolumnie nadać typ timestamp lub w innym przypadku dodana zostanie kolumna o nazwie timestamp - stąd taki typ może mieć tylko jedna kolumna w tabeli).




<blockquote>
<p>MS SQL: timestamp != datetime</p>
</blockquote>







Timestamp jest niczym innym jak znacznikiem czasowym określającym ostatnią aktualizację na rekordzie. Jednakże w MS SQL timestamp nie jest  wcale znacznikiem czasu, a ośmioznakowa tablicą binarna. Co więcej, nie ma sposobu, aby zrzutować timestampa w MSSQL na datetime (o co wiele osób pyta w sieci). Jest to niemożliwe z tego powodu, iż nie ma on nic wspólnego z czasem. Jest to inkrementowalny licznik na poziomie bazy. Dzięki temu, aby zapamiętać stan zmian w bazie, nie trzeba przetrzymywać kilku zmiennych dla każdej z tabel, a wystarczy jedna.





<blockquote>
<p>MS SQL: timestamp == rowversion</p>
</blockquote>




W celu przekonania się, że timestamp to inkrementowalna liczba całkowita, wystarczy w danej tabeli tą kolumnę zrzutować na np.  *bigint* . Stąd zapewne zalecane jest już, aby kolumnę tą nie nazywać timestamp, a rowversion. Zapewne zamiana nazw nie spowoduje niepotrzebnego nieporozumienia, a przy okazji lepiej opisuje, czym jest ta kolumna. 


Mam nadzieję, że ten krótki,  ale bogaty w treść wpis, pozwoli uniknąć pomyłek w czasie tworzenia struktur zarządzających baza danych lub hurtownią danych. 