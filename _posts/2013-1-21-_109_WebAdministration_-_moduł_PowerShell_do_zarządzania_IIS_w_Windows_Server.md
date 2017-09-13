---
layout:     post
title:      WebAdministration - moduł PowerShell do zarządzania IIS w Windows Server
date:       2013-01-21 18:07:00
summary:    Nadal będzie o alternatywnej (bez użycia GUI) konfiguracji IIS w Windows Server. Wcześniejszy wpis poświęciłem narzędziu AppCmd (AppCmd - zarządzanie IIS z wiersza poleceń w Windows Server). Bardzo poręczny i bogaty w możliwości program do nadzorowania IIS z systemowej konsoli. Ten wpis przedstawia ...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_6" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_6" checked="checked" value="64"><label for="chkTagsList_6">porady</label> <input id="chkTagsList_10" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_10" checked="checked" value="1024"><label for="chkTagsList_10">serwery</label>
---



Nadal będzie o alternatywnej (bez użycia GUI) konfiguracji IIS w Windows Server. Wcześniejszy wpis poświęciłem narzędziu AppCmd ([AppCmd - zarządzanie IIS z wiersza poleceń w Windows Server](http://www.dobreprogramy.pl/djfoxer/AppCmd-zarzadzanie-IIS-z-wiersza-polecen-w-Windows-Server,38643.html)). Bardzo poręczny i bogaty w możliwości program do nadzorowania IIS z systemowej konsoli. Ten wpis przedstawia zaś moduł WebAdministration w PowerShellu. Dzięki niemu można również kontrolować działanie IISa, ale z jeszcze większymi możliwościami konfiguracji dzięki temu co oferuje PS.




## Przygotowanie do pracy


Aby móc zacząć pracę należy uruchomić PowerShella na prawach administratora. Aby załadować omawiany moduł wpisujemy:


```ps
Import-Module WebAdministration
```


Jeśli nie chcemy za każdym razem ładować modułu w PowerShellu, wystarczy, iż utworzymy następujący skrót (oczywiście uruchamiany z prawami administratora):


```ps
%SystemRoot%\system32\WindowsPowerShell\v1.0\powershell.exe -noexit -command "import-module webadministration"
```


Podczas tworzenia skryptów warto jednak używać Windows PowerShell ISE (Integrated Scripting Environment). Uprzyjemnia pracę w pisaniu dzięki zakładkom, debugowaniu, czy dynamicznemu intellisense. Znajdziemy go w :  *%SystemRoot%\system32\WindowsPowerShell\v1.0\powershell_ise.exe*  


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-1-21-_109_/g_-_608x405_-_-_38739x20130120224054_0.png)



Dostępne polecenia znajdziemy szybko poprzez:


```ps
Get-Command -Module WebAdministration
```


Pomoc do każdego polecenia dostajemy wpisując:

```ps
Get-Help [polecenie cmdlet]
```




## Hierarchia


WebAdministration posiada hierarchę na wzór tego jak jest  w IIS:


  * IIS



  * AppPools


  * [MyAppPool]


  * WorkerProcess








  * Sites


  * [MySite]





  * SslBindings






Każdy z elementów drzewa jest wirtualnym folderem. Działają zatem polecenia  *dir*  czy  *cd* .



Poleceń  modułu jest dokładnie 79 i w połączeniu ze składnią PowerShella dają one duże pole do popisu dla osób tworzących skrypty. Moduł WebAdministration pozwala na zarządzanie każdym elementem IIS. Tworzenie witryn, aplikacji, puli aplikacji, wirtualnych folderów, backupu, konfiguracji i wszelkie manipulacje nimi. Pokazanie wszystkich możliwości modułu zajęłoby zapewne potężny rozdział w grubej książce. W tym wpisie przedstawię kilka prostych przykładów i na końcu skrypt, który będzie korzystał z omawianych poleceń. 



## Przykłady





  * nowa witryna



```ps
New-Item IIS:\Sites\Test -bindings @{protocol="http";bindingInformation=":80:Test"} -id 6 -physicalPath c:\PUB\d1
```

Wyjaśnienia wymaga zapewne użycie hash tabeli. Otóż ze względu na to, iż powiązania są w formie  *Klucz - Wartość* , taki sposób tworzenia jest bardziej uniwersalny i przyszłościowy (np. rozszerzenie poddrzewa  *binding*  o dodatkowe elementy).

  * tworzenie aplikacji



```ps
New-Item 'IIS:\Sites\Test\a1' -physicalPath c:\PUB\d\a1 -type Application
```



  * puli aplikacji 



```ps
New-Item AppPools\apool
```


  * przypisanie pula aplikacji 


```ps
Set-ItemProperty IIS:\Sites\Test\a1 -name applicationPool -value apool
```


  * skrypt do zatrzymywania/uruchamiania witryn dostępnych w IIS

Aby pokazać jak dużo, w miarę niewielkim nakładem pracy, można zrobić w PowerShellu używając modułu do zarządzania IIS, stworzę przykładowy skrypt. Jego zadaniem będzie listowanie dostępnych witryn na IIS. Użytkownik będzie mógł podać, która witryna ma zostać zatrzymana/uruchomiona (skrypt sam zatrzyma uruchomioną witrynę i uruchomi już działającą). Poniżej zamieszczam skrypt z komentarzami:


```ps
Import-Module WebAdministration

do {
    #Pobranie listy dostępnych witryn.
    #Dzięki temu, iż moduł do IIS tworzy wirtualny katalog IIS,
    #można użyć standardowej metody Get-ChildItem - listowanie zawartości folderu.
    $values = Get-ChildItem("IIS:\Sites\")
    $no = 0
    $sites = @{}

    Write-Host ""
    Write-Host "Dostępne witryny:"
    Write-Host ""
    Write-Host "--------------------"

    foreach ($item in $values){
        #W pętli wypisujemy na ekran zawartość folderu IIS.
        #Dodatkowo zapamiętujemy w zmiennej słownikowej id witryny i jej nazwę.
        $no++
        $sites.Add($no.ToString(),$item.Name) 
        Write-Host "$($no) - $($item.Name) ($($item.State),$($item.PhysicalPath))"
    }

    Write-Host "--------------------"
    Write-Host ""

    $input = "";


    #Kręcimy się w pętli, aż użytkownik nie poda pasującego ID 
    #lub zechce wyjść ze skryptu ("koniec").
    do {
        $input = Read-Host 'wybierz ID aplikacji do zmiany ("koniec" zamyka skrypt)'
    }while ($input -ne "koniec" -band $sites.ContainsKey($input) -eq $false)

    if($input -eq "koniec"){
        exit
    }

    #Pobieramy wybraną witrynę po ID, a następnie uruchamiamy lub zatrzymujemy ją.
    $selected = $sites[$input]
    if((Get-WebSite -name $selected).State -eq "Stopped"){
        Start-Website -name $selected
        Write-Host "uruchomiono $($selected)"
    }
    else{
        Stop-Website -name $selected
        Write-Host "zatrzymano $($selected)"
    }
}
while (1)






```






## Podsumowanie



Moduł WebAdministration do PowerShella, to kolejny po [AppCmd](http://www.dobreprogramy.pl/djfoxer/AppCmd-zarzadzanie-IIS-z-wiersza-polecen-w-Windows-Server,38643.html) sposób na zarządzanie IIS bez użycia GUI. Duże możliwości jakie oferuje PS sprawiają, iż jest to wyśmienite narzędzie do tworzenia zarówno prostych jak i zaawansowanych skryptów z modułem WebAdministration.