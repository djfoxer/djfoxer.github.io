---
layout:     post
title:      Project My Screen - udostępnianie ekranu Windows Phone 8.1 na ekran komputera po kablu USB
date:       2014-04-19 01:48:00
summary:    Zapewne od początku istnienia Windows Phone użytkownicy zastanawiali się w jaki sposób można przekazywać obraz ze smartfonu na ekran komputera. Atmosferę podgrzewa sam Microsoft, który przy każdej prezentacji przy użyciu urządzenia z mobilnym systemem, używał przekazywania ekranu z telefonu do aplikacji na PC lub rzutnika poprzez kabel USB. <!----><!---->Za złotych czasów homebrew na Windows Phone...
categories: oprogramowanie porady urządzenia mobilne
slug: Project-My-Screen-udostepnianie-ekranu-Windows-Phone-8.1-na-ekran-komputera-po-kablu-USB,53799.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010900_0.jpg
---



Zapewne od początku istnienia Windows Phone użytkownicy zastanawiali się w jaki sposób można przekazywać obraz ze smartfonu na ekran komputera. Atmosferę podgrzewa sam Microsoft, który przy każdej prezentacji przy użyciu urządzenia z mobilnym systemem, używał przekazywania ekranu z telefonu do aplikacji na PC lub rzutnika poprzez kabel USB. 


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010900_0.jpg)



Za złotych czasów homebrew na Windows Phone 7, udało się przygotować odpowiednie sterowniki, które pozwalały na przesyłanie obrazu po USB. Niestety wymagało to specjalnie do tego celów przygotowanego ROMu i dostępne było tylko na kilka urządzeń.

W międzyczasie Nokia stworzyła aplikację [Nokia Beamer](http://www.dobreprogramy.pl/Nokia-Beamer-udostepnianie-ekranu-Lumii-poprzez-siec,News,51800.html)  do udostępniania obrazu poprzez internet. Nie działało jednak to do końca idealnie i nie przypadło to do gustu wszystkim użytkownikom. 

Premiera Windows Phone 8.1 przynosi jednak długo oczekiwaną funkcję udostępniania ekranu na zewnętrzne źródło obrazu. Miracast działa po kablu USB (wszystkie urządzenia)  lub bezprzewodowo (tylko dla wybranych smartfonów). 

Dopiero jednak dziś dostaliśmy aplikację do udostępniania ekranu bezpośrednio na ekran komputera po kablu USB. Oto opis jak tego dokonać.



## Project My Screen - nasz ekran smartfona na PC


Aplikacja służąca do  *odbierania*  obrazu z naszego Windows Phone 8.1 nazywa się  *Project My Screen*  ( *wyświetl mój ekran* ) i dostępna jest już [do pobrania](http://download.microsoft.com/download/A/2/7/A271EFFF-6C9E-4E9B-9259-0F72FDEDD153/ProjectMyScreenApp.msi). 


Obsługa jest trywialnie prosta. Wystarczy pobrać aplikację z powyższego linku i ją zainstalować. Po uruchomieniu naszym oczom ukaże się taki oto widok (polecam wyjść z trybu pełnoekranowego poprzez wciśnięcie przycisku  *ESC* ):


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010856_0.png)


W tym momencie należy podłączyć kablem USB nasz smartfon z Windows Phone 8.1 do komputera. Na ekranie telefonu ukaże się pytanie o pozwolenie na udostępnienie ekranu:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010854_0.jpg)


Zgoda spowoduje rozpoczęcie  *transmisji*  naszego ekranu na komputer:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010859_0.png)



Całość działa szybko i niezmiernie płynnie. Co ważne, za pomocą aplikacji Project My Screen możemy sterować telefonem z poziomu PC. W opcjach na smartfonie możemy dodatkowo uruchomić wyświetlanie miejsca dotyku, a także wyjściową orientację ekranu.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010845_0.jpg)


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010852_0.jpg)




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010853_0.jpg)





## Project My Screen - problemy?


Jeśli ekran nie wyświetla się na komputerze, smartfon nie pyta się o zgodę na przekazanie obrazu, to znaczy, że w systemie posiadamy stare sterowniki do urządzenia z Windows Phone. Aby to naprawić należy usunąć (odinstalować) stare oprogramowanie. 

Na początku odłączmy smartfon od PC. Następnie otwieramy Menedżer urządzeń i z menu  *Widok*  zaznaczamy pokazywanie ukrytych urządzeń. W kolejnym kroku z menu  *Urządzenia przenośne*  usuwamy wpis o naszym smartfonie. W poddrzewku  *Urządzenia uniwersalnej magistrali szeregowej*   usuwamy stare wpisy związane z urządzeniem.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2014-4-19-_82_/g_-_-x-_-_-_x20140419010855_0.png)



Po tej operacji podłączamy ponownie smartfon z Windows Phone. Wszystko powinno działać bezproblemowo.