---
layout:     post
title:      PowerShell i .NET z GUI - programowanie w konsoli Windows Server
date:       2013-01-28 19:29:00
summary:    Niedawny wpis o administracji IIS z linii komend (WebAdministration - moduł PowerShell do zarządzania IIS w Windows Serv... ) zahaczał o dość uniwersalny moduł konsoli PowerShell. Mimo, że wydaje się, iż jest on klasycznym językiem skryptowym, w rzeczywistości jest dużo bardziej złożony i zaawansowany! W przeciwieństwie do narzędzi z grupy wiersza poleceń, w PowerShellu możemy korzystać z obiektów...
categories: porady programowanie serwery
slug: PowerShell-i-.NET-z-GUI-programowanie-w-konsoli-Windows-Server,38836.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-1-28-_121_/g_-_-x-_-_-_x20130127234112_0.png
---



Niedawny wpis o administracji IIS z linii komend ([WebAdministration - moduł PowerShell do zarządzania IIS w Windows Server](http://www.dobreprogramy.pl/djfoxer/WebAdministration-modul-PowerShell-do-zarzadzania-IIS-w-Windows-Server,38739.html) ) zahaczał o dość uniwersalny moduł konsoli PowerShell. Mimo, że wydaje się, iż jest on klasycznym językiem skryptowym, w rzeczywistości jest dużo bardziej złożony i zaawansowany! W przeciwieństwie do narzędzi z grupy wiersza poleceń, w PowerShellu możemy korzystać z obiektów .NET, WMI, czy COM. Daje to ogromne możliwości. 


PowerShell w całości działa na platformie .NET, stąd można spokojnie używać klas dostępnych np. w C#. Poniżej zaprezentuję kilka poleceń pokazujących tą zależność. 




## Obiekty




Klasyczny przykład to dobrze znane polecenie  *dir*  (listowanie katalogu). Wykorzystajmy przetwarzanie potokowe i metodę  *Get-Member*  (listowanie właściwości i zmiennych dla obiektu):



```powershell
dir | Get-Member

   TypeName: System.IO.FileInfo

Name                      MemberType     Definition                                                          
----                      ----------     ----------                                                          
Mode                      CodeProperty   System.String Mode{get=Mode;}                                       
AppendText                Method         System.IO.StreamWriter AppendText()                                 
CopyTo                    Method         System.IO.FileInfo CopyTo(string destFileName), System.IO.FileInf...
Create                    Method         System.IO.FileStream Create()                                       
CreateObjRef              Method         System.Runtime.Remoting.ObjRef CreateObjRef(type requestedType)     
CreateText                Method         System.IO.StreamWriter CreateText()                                 
Decrypt                   Method         void Decrypt()                                                      
Delete                    Method         void Delete()                                
(...)

```



Jak widać  *dir*  jest niczym innym jak obiektem typu  *System.IO.FileInfo* . Obiekt posiada metody takie jak klasa w C#. 



## Zmienne



Sprawdźmy teraz co się kryje pod zmiennymi w PowerShellu. 



```powershell
$tmp = 45.5

$tmp | Get-Member

   TypeName: System.Double

Name        MemberType Definition                                                                            
----        ---------- ----------                                                                            
CompareTo   Method     int CompareTo(System.Object value), int CompareTo(double value), int IComparable.Co...
Equals      Method     bool Equals(System.Object obj), bool Equals(double obj), bool IEquatable[double].Eq...
GetHashCode Method     int GetHashCode()                                                                     
GetType     Method     type GetType()                                                                        
GetTypeCode Method     System.TypeCode GetTypeCode(), System.TypeCode IConvertible.GetTypeCode()             
ToBoolean   Method     bool IConvertible.ToBoolean(System.IFormatProvider provider)                          
(...)

```



Zaskoczenia nie ma. Utworzona zmienna to obiekt klasy Double z .NET.



## Skrypt PowerShell + .NET



A teraz mały skrypt, wykorzystujący obiekty klas prosto z .NET. Nasz mały "programik" ma następujące założenia:



  * pobieranie określonej strony www

  * zapis pobranej strony do określonego pliku (nazwa pliku posiada aktualną datę) w celu archiwizacji (dla ułatwienia analizy, pliki zapisywane są w tym samym folderze co skrypt)

  * losowanie czasu na jaki skrypt zostanie uśpiony (losowy okres, aby nie wywołać podejrzeń ;) )

  * całość działa w pętli przez pewien zadany czas



Skrypt realizujący powyższe założenia wygląda następująco (dodatkowe informacje ułatwiające zrozumienie skryptu zawarte są w komentarzach):



```powershell

#na początku zapamiętujemy datę uruchomienia skryptu
$start =  Get-Date
#zmienne (minuty) określające w jakim przedziale, losowany będzie czas uśpienia skryptu 
$sleepTimeMin = 10
$sleepTimeMax = 40
#jak długo ma działać skrypt (w tym przypadku 24 godziny)
$howLong = 24*60
#tworzymy instancję klasy Random z .NET do losowania czasu snu
$rand = New-Object System.Random

do{
    $now = Get-Date
    #tworzymy obiekt WebClient z .NET do pobiernia danych z www
    $wc = New-Object System.Net.WebClient

    Write-Host "zaczyna pracę"

    #pobranie strony www
    $data = $wc.DownloadString("http://www.dobreprogramy.pl/djfoxer")
    #zapis pobranych danych do pliku, który w nazwie zawiera aktualną datę
    $data >> "downloaded $($now.ToString().Replace(':','.')).html"

    #losowanie czasu uśpienia
    $sleepTime = $rand.Next($sleepTimeMin, $sleepTimeMax)

    #uśpienie skryptu (domyślnie parametrem wejściowym Start-Sleep są sekundy)
    Write-Host "zasypiam na $($sleepTime) minut..."
    Start-Sleep ($sleepTime * 60)
    Write-Host "budzenie!"

#sprawdzenie, czy wybudzony skrypt nie powinien już zakończyć działanie
}while(($now - $start).TotalMinutes -lt $howLong)

Write-Host "koniec"

```



Przykładowy skrypt pokazał jak można polecenia PowerShella połączyć z obiektami prosto z .NET. Dzięki temu, w prosty i szybki sposób można stworzyć wydajne skrypty, które mają olbrzymie możliwości. Znajomość tego typu zależności z .NET dla zaawansowanego administratora, może okazać się zbawienna i nieraz pozwoli zaoszczędzić czas i ułatwi pracę w środowisku serwerowym.



## GUI


Skoro PowerShell to .NET, więc można spróbować stworzyć w nim GUI używając obiektów z frameworku. Do wyboru mamy WinForms lub WPF. Skupię się głównie na tej pierwszej opcji. Skrypt z WinForms wygląda podobnie, wręcz identycznie, jak plik  *designer*  generowane np. przez Visual Studio. 

Przedstawię teraz mały skrypt, który korzysta z GUI pod PowerShellem. Jego zadaniem będzie listowanie za pomocą polecenia  *dir*  zawartości folderu. Ścieżkę do katalogu nie będziemy podawali w konsoli, ale w polu tekstowym w oknie graficznym aplikacji PowerShell. Uruchomienie polecenia nastąpi po naciśnięciu odpoweidniego przycisku. Zawartość zostanie przedstawiona w kontrolce  *listbox* . Ostatnim elementem na formatce jest przycisk do zamknięcia okna. 

Kod z komentarzami omawiającymi poszczególne elementy skryptu, przedstawia się następująco:



```powershell

#tworzymy instancję okna
$form = New-Object System.Windows.Forms.Form
#okno otrzymuje nazwę, rozmiar oraz pozycję (środek ekranu)
#podobne właściwości otrzymują pozostałe obiekty wrzucane na okno
$form.Text = "PowerShell GUI Test"
$form.Size = New-Object System.Drawing.Size(500,520)
$form.StartPosition = "CenterScreen"

#dodajemy listę, na której będą wyśwetlać się elementy
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Size(5,50)
$listBox.Size = New-Object System.Drawing.Size(470,400) 
$form.Controls.Add($listBox)

#dodajemy przyciski do zamknięcia okna
$close = New-Object System.Windows.Forms.Button
$close.Location = New-Object System.Drawing.Size(0,450)
$close.Size = New-Object System.Drawing.Size(100,30)
$close.add_click({$form.Close()})
$close.Text = "Zamknij"
$form.Controls.Add($close)

#dodajemy pole tekstowe, gdzie wpisywać będziemy adres ścieżki
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Size(5,10)
$textBox.Size = New-Object System.Drawing.Size(470,100)
$form.Controls.Add($textBox)

#przycisk, który wykonuje komendę dir
#ścieżka dla polecenia brana jest z pola tekstowego textBox
$dir = New-Object System.Windows.Forms.Button
$dir.Location = New-Object System.Drawing.Size(120,450)
$dir.Size = New-Object System.Drawing.Size(100,30)
$dir.add_click({
    #po wciśnieciu przycisku "DIR" czyścimy listę
    $listBox.Items.Clear()
    #listujemy elementy w folderze podanym w polu tekstowym
    $values = dir -Path $textBox.Text
    #wrzucamy elementy na listę
    foreach ($item in $values){
        $listBox.Items.Add($item.Name)
    }
})
$dir.Text = "DIR"
$form.Controls.Add($dir)


$form.ShowDialog()

```





![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2013-1-28-_121_/g_-_-x-_-_-_x20130127234112_0.png)



Kilkoma poleceniami w PowerShell stworzyliśmy proste środowisko GUI dla administratora. Idealne jeśli pewne skrypty mają być obsługiwane przez osoby, które nie muszą mieć dużej wiedzy w PowerShellu, czy znać wszystkie składniki metod. Co więcej, w takiej sytuacji można wykluczyć część błędów i zmniejszyć ryzyko nieodpowiedniego użycia poleceń.

Oczywiście na początku tworzenie GUI pod PowerShella wydaj się lekko skomplikowane. Na szczęście powstało kilka narzędzi, ułatwiających tworzenie graficznych interfejsów do PowerShella. Dzięki edytorom typu WYSIWYG (ang. What You See Is What You Get) wyklikanie GUI nie powinno nastarczyć problemów. Listę narzędzi można znaleźć pod adresem: [PowerShell GUIs](http://social.technet.microsoft.com/wiki/contents/articles/4579.powershell-guis.aspx).  



## Podsumowanie


Znajomość .NET dla zaawansowanych administratorów wydaje się rzeczą bardzo atrakcyjną. Nie tylko zwiększa szybkość i komfort pracy, dzięki skryptom o większych możliwościach, ale także pozwala na proste tworzenie własnych skryptów z GUI. Bardziej przyjazny interfejs idealnie nada się dla mniej doświadczonych osób, które muszą skorzystać ze skryptów i przy okazji pełnić może formę walidatora. Warto znać wszystkie możliwości PowerShella, aby móc pracować efektywniej, szybciej i prościej.