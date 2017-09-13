---
layout:     post
title:      Konfigurujemy Unit Test w Universal Windows Platform
date:       2016-05-31 23:49:00
summary:    Do każdego projektu w Universal Windows Platform możemy dodać test jednostkowy, niezbędny do dewelopingu nowych rzeczy, czy naprawy błędów.Taki test zapewne w wielu przypadkach będzie wymagał dodania konfiguracji, aby nie hardcodować na sztywno parametrów niezbędnych do działania (np. danych do logo...
categories: windows programowanie urządzenia mobilne
---



Do każdego projektu w Universal Windows Platform możemy dodać test jednostkowy, niezbędny do dewelopingu nowych rzeczy, czy naprawy błędów.

Taki test zapewne w wielu przypadkach będzie wymagał dodania konfiguracji, aby nie hardcodować na sztywno parametrów niezbędnych do działania (np. danych do logowania). W tym celu można podać potrzebne parametry ( *klucz -wartość* ) w pliku, z którego będą zaczytywane niezbędne informacje podczas uruchomienia Unit Testu.

Taki plik jest niezależny od kodu, a zatem nie musi być dorzucany do otwartego repozytorium. Dzięki temu poufne dane, jak np. login i hasło do konta na dobrychprogramach, które pozwalają na testowanie DePeszy, nie będą udostępniane na zewnątrz. Zatem do dzieła!



### Plik z parametrami w XML - konfiguracja



Plik z parametrami  *klucz - wartość*  jest następującym w formacie XML :


```xml

&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;RunSettings&gt;
  &lt;!-- Parameters used by tests at runtime --&gt;
  &lt;TestRunParameters&gt;
    &lt;Parameter name=&quot;dpTestLogin&quot; value=&quot;LOGIN&quot; /&gt;
    &lt;Parameter name=&quot;dpTestPassword&quot; value=&quot;HASŁO&quot; /&gt;
  &lt;/TestRunParameters&gt;
&lt;/RunSettings&gt;

```


Łączymy go z testami w naszej solucji za pomocą menu w Visual Studio w  *Test-&gt;Test Settings i Select Test Settings File.*  Umieściłem go w projekcie  *djfoxer.dp.notification.Test*  jako plik  *test.runsettings* , z wyłączeniem z Gita.



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_37_/g_-_608x405_-_-_73645x20160601012035_0.PNG)



Od tej chwili uruchomiony test będzie wiedział skąd ma pobierać dane konfiguracyjne.



### Użycie danych w testach



Teraz w kodzie odwołujemy się do danych w XML za pomocą zmiennej  *Properties*  w obiekcie  *TestContext*  w klasach testowych ( *TestClass* ):


```csharp


 
```

    public class UnitTest1
    {
        private static TestContext _testContext;
        private static DpLogic logic = null;

        [ClassInitialize]
        public static void SetupTests(TestContext testContext)
        {
            _testContext = testContext;
            logic = new DpLogic();
        }

        [TestMethod]
        private voidLogin()
        {
            Tuple&lt;bool, DateTime?&gt; success = null;

            Task.Run(async () =&gt;
            {
                success = await logic.SetSessionCookie(
                    _testContext.Properties[&quot;dpTestLogin&quot;].ToString(),
                    _testContext.Properties[&quot;dpTestPassword&quot;].ToString()
                    );
            }).GetAwaiter().GetResult();

            Assert.AreNotEqual(success.Item1, false);

        }

    }
[/code]

Elegancko i bez zbędnych poufnych danych w kodzie. Kod łatwy do dowolnej parametryzacji, bez zmian w kodzie, z zachowaniem bezpieczeństwa. Oczywiście pamiętajmy, aby pliki XML z danymi dodać do ignorowanych w konfiguracji repozytorium.



<blockquote>
<p>DePesza dostępna jest w markecie Windows 10 (desktop i mobile). Bezpośredni link: [DePesza](https://www.microsoft.com/pl-pl/store/apps/depesza/9nblggh4nvs2).</p>
</blockquote>

<blockquote>
<p>Aktualne źródła można znaleźć na GitHub pod adresem:
[https://github.com/djfoxer/dp.notification](https://github.com/djfoxer/dp.notification)</p>
</blockquote>


![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2016-5-31-_37_/g_-_608x405_-_-_73645x20160601012025_0.png)

