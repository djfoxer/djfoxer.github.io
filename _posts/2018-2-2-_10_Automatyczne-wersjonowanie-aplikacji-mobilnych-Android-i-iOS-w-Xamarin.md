---
layout:     post
title:      Automatyczne wersjonowanie aplikacji mobilnych Android i iOS w Xamarin
date:       2018-02-02 20:05:00
summary:    Xamarin pozwala na tworzenie aplikacji pod Androida i iOS używając jedynego słusznego języka programowania, czyli C# ;) Jednym z częstszych problemów na jakie się natkniemy podczas wrzucania naszych apek do marketów jest wersjonowanie aplikacji. W jaki sposób jednocześnie numerować kolejne wydania pod Androida i iOS, bez szukania za każdym razem plików, a także sterować numeracją tylko z jednego m...
categories: porady programowanie urządzenia mobilne
slug: Automatyczne-wersjonowanie-aplikacji-mobilnych-Android-i-iOS-w-Xamarin,85853.html
img: https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2018-2-2-_10_/g_-_-x-_-_-_x51fcb691-dbf3-49cf-a39c-1307f1c9db30.png
---



Xamarin pozwala na tworzenie aplikacji pod Androida i iOS używając jedynego słusznego języka programowania, czyli C# ;) Jednym z częstszych problemów na jakie się natkniemy podczas wrzucania naszych apek do marketów jest wersjonowanie aplikacji. W jaki sposób jednocześnie numerować kolejne wydania pod Androida i iOS, bez szukania za każdym razem plików, a także sterować numeracją tylko z jednego miejsca? Jest na to ciekawy sposób, poprzez eventy dostępne w  *csproj, * pliku projektu w Visual Studio.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2018-2-2-_10_/g_-_-x-_-_-_x51fcb691-dbf3-49cf-a39c-1307f1c9db30.png)



## Numeracja pod Androida


Wrzucając aplikację do marketu Google musimy pamiętać o poprawnym uzupełnieniu pliku  *AndroidManifest.xml* . Znajdują się w nim informacje odnośnie naszej aplikacji jak kompatybilność z SDK, uprawnienie i masę innych ustawień. W tym momencie interesują nas dwie właściwościowi:


  *  *android:versionCode*  - jest to numer (int) kolejnych wersji w markecie Google, nie jest on pokazywany dla użytkownika; numeracja jest dowolna, ale kolejne wydania muszą mieć rosnącą numery (np. 23, 24, itd.)



  *  *android:versionName*  - jest to wersja aplikacji (string), jaką widzi użytkownik, służy głównie do celów informacyjnych (np. 1.3.5)



## Numeracja iOS


Wersjonowanie kolejnych wydań w AppStorze jest delikatnie inne niż pod Androidem. Jednakże również w tym przypadku numerację ustalamy w specjalnym pliku, jest nim  *Info.plist* . Pod iOS musimy wziąć pod uwagę następujące pola:


  *  *CFBundleVersion * - numer (string) wewnętrzny, niewidoczny dla użytkownika; kolejne wersje muszą mieć rosnącą numerację (np. 1.3.5, 1.3.6 itd.)



  *  *CFBundleShortVersionString*  - numer (string) widoczny dla użytkownika (np 1.3.5)




## Wspólna numeracja


Na powyższym opisie widać, jasno że numeracja dla użytkownika może spokojnie być dowolnym numerem ( *android:versionName*  i  *CFBundleShortVersionString* ). W tym przypadku będziemy stosowali standardową numerację  *X.Y.Z*  

Problemem są jednak numery wewnętrzne, które są określają kolejne wersje aplikacji w markecie. Dla ułatwienia można spokojnie przyjąć, że numer  *CFBundleShortVersionString,*   *CFBundleVersion i * android:versionName będą identyczne (czyli wg schematu X.Y.Z). W celu ujednolicenia wersji również pod Androida, ustalimy odgórnie, iż numer  *android:versionCode*  będzie ostatnim numerem ze schematu, czyli Z i to on będzie podbijany przed każdą publikacją.

Zatem numeracja będzie następująca:

X.Y.Z np. 1.3.10

 *CFBundleShortVersionString = * CFBundleVersion =  *android:versionName*  = X.Y.Z

 *android:versionCode*  * * = Z

przy czym pamiętamy, że za każdym razem, przed publikacją do sklepu, będziemy zwiększali numerację Z.


## Automatyczna numeracja poprzez Visual Studio (programowanie w .csproj)


Nasza automatyczna numeracja będzie w skrócie wyglądała następująco. W jednym miejscu w solucji będziemy przechowywali numer aktualnej wersji aplikacji. Przy buildzie z tego miejsca pobieramy numer i wstrzykujemy do pliku AndroidManifest.xml w projekcie Android i Info.plist w projekcie iOS.

Ustaliliśmy zatem, iż numeracja obu aplikacji będzie wyglądała następująco: X.Y.Z. Musimy jeszcze znaleźć miejsce, gdzie będziemy przechowywali numer, skąd będziemy go wstrzykiwali do poszczególnych plików w projekcie. 

W moim przypadku solucja Xamarin posiada projekt pod Androida, iOS i co najmniej jeden projekt będący bazowym projektem skąd pobierać będziemy numer (tutaj XamarinApp.Core). Użyłem do demonstracji Xamarina natywnego, ale równie dobrze może być to Xamarin.Forms, nie ma to znaczenia.


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2018-2-2-_10_/g_-_-x-_-_-_xf638d1d3-8a73-4f67-bafb-a2a7d49cf17d.PNG)


Numer wersji umieścimy w  *AssemblyInfo.cs:* 




```csharp
[assembly: AssemblyVersion("1.2.5.0")]
```


jednakże będziemy pobierali stąd tylko trzy pierwsze numery (czyli 1.2.5), a ostatni z tej trójki będzie służył jako numer do  *versionCode * do Androida i będzie musiał być podbijany za każdym razem, gdy zechcemy wrzucić apkę do marketu.

Kolejnym krokiem jest edycja plików .csproj dla Androida i iOS tak, aby przy buildzie pobierał z dll projektu (XamarinApp.Core, w którym mamy numerację globalną) numer wersji, a następnie obrabiał ją i wstrzykiwał do odpowiednich plików.


### Autonumeracja w projekcie iOS


Zaczniemy od solucji iOS. W dowolnym edytorze otwieramy plik csproj dla projektu iOS. Przechodzimy na sam koniec pliku XML i tuż przed końcem zamknięciem tagu  *</Project>*  dodajemy własny kod:




```xml
<Target Name="BeforeBuild"> 
    <GetAssemblyIdentity AssemblyFiles="..\XamarinApp.Core\bin\$(Configuration)\XamarinApp.Core.dll"> 
      <Output TaskParameter="Assemblies" ItemName="AssemblyInfo" /> 
    </GetAssemblyIdentity> 
    <PropertyGroup> 
      <FullNumber>%(AssemblyInfo.Version)</FullNumber> 
      <VersionNumber>$([System.Text.RegularExpressions.Regex]::Match(%(AssemblyInfo.Version), 
       `[^.][^.]*.[^.]*.[^.]*`))</VersionNumber> 
    </PropertyGroup> 
    <XmlPoke XmlInputPath="..\XamarinApp.iOS\Info.plist" 
       Query="//dict/key[. = 'CFBundleVersion']/following-sibling::string[1]"
       Value="$(VersionNumber)" /> 
    <XmlPoke XmlInputPath="..\XamarinApp.iOS\Info.plist" 
       Query="//dict/key[. = 'CFBundleShortVersionString']/following-sibling::string[1]"
       Value="$(VersionNumber)" /> 
 </Target>
```


W tym przypadku określamy, że przed buildem danego projektu mobilnego ( *Name=BeforeBuild* ) będziemy pobierali z określonej dll  *AssemblyInfo * (XamarinApp.Core builduje się jako pierwsze), a z niej numer w  *AssemblyVersion* . Z numeru tego wyodrębniamy za pomocą Regexu trzy pierwsze numery i przypiszemy go do "zmiennej"  *VersionNumber* . 

Mając już numer otwieramy plik Info.plist, który jest typu XML i wstrzykujemy w odpowiednie pola  *CFBundleVersion*  i CFBundleShortVersionString numer z VersionNumber (użycie  *XmlPoke* ). 


### Autonumeracja w projekcie Android


Bardzo podobnie wygląda sprawa z solucją Androidową. Tu również edytujemy plik .csproj




```xml
<Target Name="AfterBuild"> 
    <GetAssemblyIdentity AssemblyFiles="..\XamarinApp.Core\bin\$(Configuration)\XamarinApp.Core.dll"> 
      <Output TaskParameter="Assemblies" ItemName="AssemblyInfo" /> 
    </GetAssemblyIdentity> 
    <PropertyGroup> 
      <FullNumber>%(AssemblyInfo.Version)</FullNumber> 
      <VersionNumber>$([System.Text.RegularExpressions.Regex]::Match(%(AssemblyInfo.Version),
	`[^.][^.]*.[^.]*.[^.]*`))</VersionNumber> 
      <BuildNumber>$(FullNumber.Split('.')[2])</BuildNumber> 
    </PropertyGroup> 
    <XmlPoke XmlInputPath="..\XamarinApp.Android\Properties\AndroidManifest.xml"
	Namespaces="&lt;Namespace Prefix='android' Uri='http://schemas.android.com/apk/res/android' /&gt;"
	Query="manifest/@android:versionCode" Value="$(BuildNumber)" />
    <XmlPoke XmlInputPath="..\XamarinApp.Android\Properties\AndroidManifest.xml"
	Namespaces="&lt;Namespace Prefix='android' Uri='http://schemas.android.com/apk/res/android' /&gt;"
	Query="manifest/@android:versionName" Value="$(VersionNumber)" />
 </Target>
```


 W tym przypadku również pobieramy wersję z  *AsseblyInfo* , ale dodatkowo tworzymy nową "zmienną"  *BuildNumer* , która jest ostatnim numerem z trzy-liczbowej wersji zapisanej w  *FullNumber* . 

Podobnie jak na iOS, otwieramy plik XML z ustawieniami aplikacji do marketu (tym razem to plik AndroidManifest.xml) i wstrzykujemy  *BuildNumer * pod pole  *versionCode* , a  *VersionNumber * pod  *versionName* .

W ten oto sposób sterujemy numeracją aplikacji na iOS i Androida w projekcie Xamarin z jednego miejsca, z uwzględnieniem wymagań poszczególnych sklepów mobilnych.


## Na koniec


Zapanowanie nad numeracją aplikacji poprzez "programowanie w csproju" jest świetnym sposobem na pomoc w dewelopowaniu pod Xamarina. Spokojnie można także dodać numerację dla aplikacji UWP, jeśli zaszłaby taka potrzeba. Można również numer wersji trzymać w oddzielnym pliku xml, a wstrzykiwanie numerów dodać do jednego tylko csproja, który będzie podmieniał wersja dla dwóch różnych projektów mobilnych. Możliwości jest dużo.

Mam nadzieję, że wpis będzie pomocny przy tworzeniu kolejnych wersji aplikacji mobilnych w Xamarinie. 