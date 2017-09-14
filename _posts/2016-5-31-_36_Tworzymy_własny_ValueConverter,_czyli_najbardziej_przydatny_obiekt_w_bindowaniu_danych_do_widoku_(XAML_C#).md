---
layout:     post
title:      Tworzymy własny ValueConverter, czyli najbardziej przydatny obiekt w bindowaniu danych do widoku (XAML/C#)
date:       2016-05-31 23:57:00
summary:    Zapewne tworząc aplikacje w WPF czy UWP natknęliście się na to, że właściwość w modelu (ViewModelu) wymagała konwersja na inny typ lub inną wartość, aby móc jej użyć na widoku. Tworzenie jednak dodatkowych właściwości jest nieefektywne i zbędne. Z pocą przychodzi interfejs IValueConverter, który konwertuje jedne dane na drugie, bez konieczność rozszerzania obiektu. W moim przypadku musiałem przekw...
categories: windows oprogramowanie programowanie
---



Zapewne tworząc aplikacje w WPF czy UWP natknęliście się na to, że właściwość w modelu (ViewModelu) wymagała konwersja na inny typ lub inną wartość, aby móc jej użyć na widoku. Tworzenie jednak dodatkowych właściwości jest nieefektywne i zbędne. 

Z pocą przychodzi interfejs  *IValueConverter* , który konwertuje jedne dane na drugie, bez konieczność rozszerzania obiektu. W moim przypadku musiałem przekwaterować status notyfikacji NotificationStatus (New, Old, Unknown) na Opacity (nieprzezroczystość).

Na widoku nowe powiadomienia nie są przezroczyste, zaś stare mają przezroczystość ustawioną na 0.5. Efekt jest następujący:


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_36_/g_-_608x405_-_-_73651x20160601002238_0.png)


Oczywiście najbardziej używanym konwerterem jest: Bool <=> Visibility, czyli mając zmienną o typu Bool(true/false), chcemy sterować widocznością elementu (Visibility.Visible/Visibility.Collapsed).Przejdźmy jednak do naszego przykładu.

Zamiast tworzyć nową właściwość, szybko tworzymy klasę implementującą interfejs IValueConverter.


```csharp

public sealed class StatusToOpacityConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, string language)
    {
        NotificationStatus status = (NotificationStatus)value;
        if (status == NotificationStatus.New)
        {
            return 1;
        }
        else
        {
            return 0.5;
        }
    }

    public object ConvertBack(object value, Type targetType, object parameter, string language)
    {
        throw new NotImplementedException();
    }
}

```


Interfejs  *IValueConverter*  wymaga implementacji dwóch metod:  *Convert*  i  *ConvertBack* .Pierwsza z nich implementuje konwersję danych z obiektu na dane niezbędne do użycia na widoku, zaś druga robi to w odwrotną stronę.

W naszym przypadku zadanie jest proste. Powiadomienie ze statusem  *NotificationStatus.New*  nie może być przezroczyste, zaś notyfikacje z innymi statusami mają otrzymać przezroczystość 0.5. Zmienna  *value*  jest zawsze typu  *NotificationStatus* , więc bez dodatkowej zabawy rzutujemy ją na ten typ i zwracamy int określający przezroczystość.

Możemy skorzystać również ze zmiennej  *targetType* , z typem zmiennej wynikowej. Dodatkowo  *parameter*  może zawierać dodatkowe informacje przesłane do konwertera z widoku. Ważnym parametrem jest także zmienna  *language* , która określa język aplikacji w chwili konwersji, do wykorzystania, gdy konwersja zależna jest od używanego języka (np. zamiana daty na string).

W drugą stronę konwersja przebiega podobnie z tym, że dane wejściowe i wyjściowe są zamienione. W omawianym przypadku na wejściu mielibyśmy zmienną  *int* , a typem wynikowym byłby  *NotificationStatus* .

Jednakże nie jest to nam potrzebne, gdyż łączenie ( *bindowanie* ) w tym przypadku obiektu (z danymi) z widokiem odbywa się w jedną stronę ( *one-way binding* ).

Na widoku, czyli w pliku XAML, konwertera użyjemy w następujący sposób:


```xml

<Grid
        Opacity="{
        Binding Status, 
        Converter={StaticResource StatusToOpacityConverter},
        Mode=OneWay
        }" 
                      
        >(...)</Grid>

```


Oczywiście obiekt  *przekazany*  do widoku ma właściwość  *Status*  o typie  *NotificationStatus* . 

Na końcu pamiętajmy jeszcze o rejestracji  *StatusToOpacityConverter*  w  *App.xaml* :


```xml

<Application
    (...)
    xmlns:helpers="using:djfoxer.dp.notification.App.Helpers">
    <Application.Resources>
        (...)
        <helpers:StatusToOpacityConverter  x:Key="StatusToVisibilityConverter"  />
    </Application.Resources>
</Application>

```




> DePesza dostępna jest w markecie Windows 10 (desktop i mobile). Bezpośredni link: [DePesza](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2).


> Aktualne źródła można znaleźć na GitHub pod adresem:
> [https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)

![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_36_/g_-_608x405_-_-_73651x20160601010129_0.png)

