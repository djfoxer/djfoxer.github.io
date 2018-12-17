---
layout:     post
title:      DevCon.exe — menedżer urządzeń z wiersza poleceń w Windows 
date:       2016-01-13 16:40:00
summary:    Menedżer urządzeń w Windows znają zapewne wszyscy, ale nie każdy może wiedzieć, iż istnieje także wersja konsolowa. DevCon.exe (Device Console ) jest narzędziem z linii wiersza poleceń, które pozwala na zarządzenie sprzętem w okienkach od Microsoftu. Aplikacja pozwala na aktywowanie/dezaktywowanie, instalację, usuwanie i bogatą konfigurację urządzeń w Windowsie. DevCon.exe jest bardziej rozbudowan...
categories: windows sprzęt porady
slug: DevCon.exe-menedzer-urzadzen-z-wiersza-polecen-w-Windows,69427.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112225023_0.jpg
---



Menedżer urządzeń w Windows znają zapewne wszyscy, ale nie każdy może wiedzieć, iż istnieje także wersja konsolowa. DevCon.exe (Device Console ) jest narzędziem z linii wiersza poleceń, które pozwala na zarządzenie sprzętem w okienkach od Microsoftu. Aplikacja pozwala na aktywowanie/dezaktywowanie, instalację, usuwanie i bogatą konfigurację urządzeń w Windowsie. DevCon.exe jest bardziej rozbudowany funkcjonalnie niż Menedżer urządzeń. Dodatkowo aplikacja pozwala na zarządzanie sprzętem na komputerze lokalnym, ale także na komputerze zdalnym.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112225023_0.jpg)






## DevCon -instalacja

 
 
DevCon.exe jest częścią Windows Driver Kit i można pobrać go z całym pakietem. DevCon działa już od Windows 2000, zaś najnowszą wersję WDK 10 można pobrać [tutaj](https://msdn.microsoft.com/en-us/windows/hardware/dn913721.aspx#wdk10).  Kod źródłowy DevCon został udostępniony za darmo przez Microsoft i można go znaleźć na [GitHubie](https://github.com/Microsoft/Windows-driver-samples/tree/master/setup/devcon).  Co ciekawe DevCon można znaleźć razem z aplikacjami innych producentów sprzętu (np. Lenovo dorzuca DevCon.exe wraz modułem do zarządzania energii - Energy Manager). DevCon posiada oddzielną wersją pod system 32 i 64 bitowy. Co ważne można obsługa z wiersza poleceń umożliwia pisanie zaawansowanych skryptów. Narzędzie do pracy wymaga uprawnień administracyjnych. 

Narzędzie, po zainstalowaniu WDK, znajduje się w folderze:



```powershell

%WindowsSdkDir%\tools\x64\devcon.exe
%WindowsSdkDir%\tools\x86\devcon.exe
%WindowsSdkDir%\tools\arm\devcon.exe

```





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160110162710_0.png)





## Praca z DevCon



Lista dostępnych komend w  DevCon.exe jest dość pokaźna i krótki opis każdej z nich otrzymamy po wpisaniu komendy

 

```powershell
devcon help
```





```powershell

classfilter          Add, delete, and reorder class filters.
classes              List all device setup classes.
disable              Disable devices.
driverfiles          List installed driver files for devices.
drivernodes          List driver nodes of devices.
enable               Enable devices.
find                 Find devices.
findall              Find devices, including those that are not currently attached.
help                 Display Devcon help.
hwids                List hardware IDs of devices.
install              Install a device manually.
listclass            List all devices in a setup class.
reboot               Reboot the local computer.
remove               Remove devices.
rescan               Scan for new hardware.
resources            List hardware resources for devices.
restart              Restart devices.
sethwid              Modify Hardware ID's of listed root-enumerated devices.
stack                List expected driver stack for devices.
status               List running status of devices.
update               Update a device manually.
updateni             Manually update a device (non interactive).
dp_add               Adds (installs) a third-party (OEM) driver package.
dp_delete            Deletes a third-party (OEM) driver package.
dp_enum              Lists the third-party (OEM) driver packages installed on machine.


```



Każde z wywołań funkcji DevCon może zostać poprzedzone przełącznikiem /r który oznaczą, iż w razie potrzeby zostanie zrestartowany komputer.



```powershell
devcon /r disable *CDROM*  # dezaktywuje napęd 
```



Każde z poleceń DevCon  posiada dodatkowy opis, ze szczegółami wywoływania, które można otrzymać poprzez wywołanie:



```powershell
devcon help <command>
```



Dostęp do konfiguracji  komputera zdalnego uzyskamy poprzez użycie parametru /m z nazwą zdalnej maszyny:



```powershell
devcon /m:\\computer
```



Devcon akceptuje w  *zapytaniach*  znak specjalny *, który pozwala na wyszukanie po częściach nazwy (komputera, ID urządzenia, klasy, instancji itd.), np.:



```powershell
devcon find *usb* *acpi*
```



Takie zapytanie zwróci urządzenia, które mają w ID  *usb*  lub  *acpi*  (użycie co najmniej dwóch elementów do wyszukiwania implikuje wyszukiwanie  *lub*  [or]).



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112221550_0.png)



Można również ograniczyć wyszukiwanie do klasy, poprzez podanie nazwy klasy np.:



```powershell
devcon hwids =usb *root* *ven*
```



Spowoduje przefiltrowanie urządzeń z klasy usb, które mają w ID nazwę  *root*  lub  *ven* .



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112221549_0.png)





### Użycie DevCon, przykład z życia wzięty



DevCon ma wiele zastosowań i zapewne wielu z was aplikacja może przydać się w przyszłości. W moim przypadku DevCon rozwiązała problem ze starą drukarką i nowymi okienkami od Microsoftu. Otóż po aktualizacji do Windows 10 (32bit) na starszym komputerze nieśmiertelna drukarka HP 710C (na porcie równoległym) sypała błędami przy próbie drukowania. Okazało się, że sterowniki HP do sprzętu zostały całkowicie  *skopane* , a  w systemach od Windows 8.x 64 bit nie można zupełnie używać tej drukarki! Na szczęście system był 32 bitowy i w tym wypadku błąd w sterownikach można było prosto ominąć. Otóż przed drukowaniem wystarczyło jedynie usunąć całkowicie sterowniki z portów LPT i ponownie je dodać. Czynność prosta, ale jednakże poprzez menedżer urządzeń wygajająca kilku kliknięć. Dodatkowo, osoby pracujące na co dzień z owym komputerem nie posiadały na tyle wiedzy, aby sobie z tym poradzić. Z pomocą przyszło narzędzie DevCon. Usunięcie i ponownie zainstalowanie urządzeń znajdujących się na porcie równoległym stało się niezmiernie proste. Stworzeniu odpowiedniego skryptu, uruchamianego poprzez dwukrotne kliknięcie, pozwalało na szybkie rozwiązanie problemu:



```powershell

devcon remove *pnp04*  #usuwamy wszystko co znajduje się na portach równoległych
devcon rescan #skanujemy w poszukiwaniu nowego sprzętu
# (sterowniki drukarki zostaną ponowie dodane)

```



Bez  *devcon* , próba obejścia problemu wymagałaby znacznie więcej wysiłku i klikania dla przeciętnego użytkownika komputera.   



### Kilka innych  przykładów użycia DevCon



Wcześniej użyłem już poleceń  *hwids*  i  *find*  do wyszukiwania ID oraz klas urządzeń, a także  *rescan*  (do odświeżenia listy podzespołów działających na Plug and Play).
Oto kilka innych zastosowań DevCon. Oczywiście to tylko mały wycinek możliwości narzędzia.

Jeśli chcemy szybo odnaleźć pliki, jakie wchodzą w skład sterownika, użyjemy polecenia  *drivefiles* :



```powershell
devcon driverfiles =media
```





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112223201_0.png)



Szczegóły pakietów sterowników odnajdziemy poprzez polecenie  *devcon* :



```powershell
devcon drivernodes =usb pci*
```





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112223201_1.png)



Status poszczególnych podzespołów uzyskamy poprzez polecenie  *status* :



```powershell
devcon status *cd*
```





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-1-13-_71_/g_-_-x-_-_-_x20160112223202_0.png)



Polecenie  *enable/disable*  aktywuje urządzenia, np:



```powershell
devcon disable =printer
```



Wymuszenie nadpisania sterowników do urządzenia z pliku INF odbywa się poprzez komendę  *update*  (polecenie  *updateNI*  nie wyświetla powiadomień):



```powershell
devcon /r update c:\windows\inf\newdvc.inf *PNP030b
```






## DevCon - mały, darmowy i z wielkimi możliwościami


DevCon.exe pozwala na szybkie tworzenie skryptów do zarządzania sprzętem zarówno na komputerze lokalnym, ale także i na maszynie zdalnej. Zapewne szeroką gamę zastosowań znajdą tutaj nie tylko administratorzy, ale również zaawansowaniu użytkownicy, którzy w trywialny sposób ułatwią sobie konfigurację, naprawę czy szczegółową diagnozę sprzętu.



