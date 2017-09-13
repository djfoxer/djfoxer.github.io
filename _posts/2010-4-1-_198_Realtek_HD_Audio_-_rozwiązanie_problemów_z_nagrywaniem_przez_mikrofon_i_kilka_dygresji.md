---
layout:     post
title:      Realtek HD Audio - rozwiązanie problemów z nagrywaniem przez mikrofon i kilka dygresji
date:       2010-04-01 11:09:00
summary:    Słowem wstępuWitam serdecznie na moim blogu. To jest pierwszy wpis, jak widać;).Chciałbym w nim poruszyć temat problemów z nagrywaniem przez mikrofon na karce Realtek HD Audio, czyli w jaki sposób zrobić:- włączenie boosta (problem: słaba słyszalność nagrywania przez mikrofon) - "naprawa" dźwięku na...
categories: <input id="chkTagsList_0" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_0" checked="checked" value="1"><label for="chkTagsList_0">windows</label> <input id="chkTagsList_3" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_3" checked="checked" value="8"><label for="chkTagsList_3">oprogramowanie</label> <input id="chkTagsList_6" type="checkbox" name="ctl00$phContentRight$chkTagsList$chkTagsList_6" checked="checked" value="64"><label for="chkTagsList_6">porady</label>
---



Słowem wstępu


Witam serdecznie na moim blogu. To jest pierwszy wpis, jak widać;).
Chciałbym w nim poruszyć temat problemów z nagrywaniem przez mikrofon na karce Realtek HD Audio, czyli w jaki sposób zrobić:
- włączenie boosta (problem: słaba słyszalność nagrywania przez mikrofon) 
- "naprawa" dźwięku nagrywanego przez mikrofon (wyłączenie rejestrowania dźwięku z komputera np. dźwięk z gry, mp3 itp., na mikrofon)  
Zapraszam do lektury :)





### Jak to się zaczęło




Najprawdopodobniej nigdy bym nie zaprzątał sobie głowy, gdyż gdy rozmawiałem na skype czy gg przez mikrofon była całkiem ok. Jednakże kupiłem niedawno grę CoD4: Modern Warfare i po przejściu świetnego, jednakże krótkiego SP, zasiadłem do MP.


Wówczas zaczął się problem. Podłączyłem słuchawki oraz mikrofon i... pozostali członkowie teamu raz, że ledwo mnie słyszeli to jeszcze słyszeli wszelkie odgłosy z gry i z komputera (np. radio/mp3)! Co powodowało czasami dziwne echo (nawet na słuchawkach!). 
Znalezienie rozwiązania trochę mi zajęło czasu, więc che podzielić się z wami. Oczywiście, nie są to jakieś kamienie milowe:P ale mam nadzieję, że się komuś przydadzą. A zatem do dzieła!




### Menadżer Realtek HD Audio - jakie to jest brzydkie

 


Programiści (może raczej designerzy) nie popisali się tworząc okno zarządzania kartą dźwiękową Realtek HD Audio. To co widzimy jest tragiczne! 

Brak skalowalności, niektóre przyciski po najechaniu myszką zmieniają kolor informując o możliwości interakcji, a niektóre nie. 
Zakładki, z racji małego okna, nie wyświetlają się wszystkie i musimy je "strzałeczkami" przewijać (a można było by umieścić je w kilu rzędach), przez co tracimy ogólny podgląd. 
Podobnie jest na zakładce Mikser, musimy na oślep klikać w "strzałki", żeby znaleźć to czego poszukujemy (wystarczyło by dodać malutki pasek przewijania).
Ogólnie nie przekonuje mnie to co zrobili panowie z Realtek'a. Ale może to tylko moje zdanie. Ok, koniec narzekań, przejdźmy do pierwszego problemu...




## Włączenie boosta (problem: słaba słyszalność nagrywania przez mikrofon)




I tutaj "kłania" się super intuicyjny interface dzieła Realtek'a. Normalnie można to zrobić w Regulacji głośności dostępny w systemie. Ale na kartach Realteka nie ma tak prosto!
Opcja jest tam nieaktywna! Takowa opcja jest ukryta w Menadżerze Realtek'a. Tylko w miejscy tak logicznym, że aż mnie ściska! Wiecie gdzie? W panelu odtwarzania dźwięku!


Aby włączyć boosta (zwiększenie wydajność mikrofonu) musisz: 
1. Otworzyć Menadżer Realtek HD Audio (ikonka czerwonego głośniczka koło zegara)
2. Przejść na zakładkę Mikser
3. W panelu Odtwarzaj klikać na strzałki, aż ujrzysz: Front Pink In, Rear Pink In
4. W zależności gdzie podpiąć mikrofon czy do panelu przedniego (Front), czy z tyłu obudowy (Rear), klikasz dla wybranej opcji w malutki przycisk, który ma dwie kropeczki: ..
5. Bingo! Mamy to! :) Okienko do włączenia zwiększenia wydajność mikrofonu! Zaznaczamy i cieszymy się tym, iż nasi rozmówcy wreszcie nasz słyszą głośno!



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-4-1-_198_/g_-_608x405_-_-_17467x20100401110221_1.png)

 



### Aktualizacja: Windows Vista/7/8



W przypadku nowych systemów Windows,boost ukryty jest w zakładce  *Mikrofon* , pod mało czytelną ikoną (zaznaczone na zrzucie ekranu): 



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-4-1-_198_/g_-_608x405_-_-_17467x20130220093911_0.jpg)





## "Naprawa" dźwięku nagrywanego przez mikrofon (wyłączenie rejestrowania dźwięku z komputera np. dźwięk z gry, mp3 itp., na mikrofon)





Nie jest to raczej duży problem, ale mimo, iż mam duże doświadczenie z komputerami to trochę mi to zajęło żeby znaleźć co trzeba zrobić, aby się pozbyć tego. Oto szybkie kroki na wyeliminowanie powyższego "ficzeru;)" : 


"Naprawa" dźwięku nagrywanego przez mikrofon (wyłączenie rejestrowania dźwięku z komputera np. dźwięk z gry, mp3 itp., na mikrofon:
1. Z meny start przechodzimy do folderu: Akcesoria -> rozrywka -> Regulacja głośności
2. W otwartym oknie z menu wybieramy opcje -> właściwości
3. W nowo otwartym oknie z comboboxa wybieramy Audio Input i klikamy na OK
4. Mając nowe okno wyciszamy wszystko oprócz: Regulacja nagrywania oraz Głośność mikrofonu
5. W taki oto sposób pozbyliśmy się nagrywania przez mikrofon inny dźwięków z komputera (mp3/radio/gry/ dźwięki systemowe i inne)



![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-4-1-_198_/g_-_608x405_-_-_17467x20100401110221_2.png)

 






## Na zakończenie





Mam nadzieję, że oba rozwiązania się przydadzą i czekam na opinie, komentarze i propozycje.
Pozdrawiam, do następnego "zczytania się" :)

P.S.
Odnośnie gry Cod4: MW, jeśli kogoś interesuje jak pozbyć się lagów w tej grze, które spowodowane są przez "rewelacyjnego" PunkBuster proszę o info w komentarzach.



## Aktualizacja




### Windows 7, 8, 10


Jeśli macie problemy na nowszych systemach, warto zainstalować aplikację [Volume2](http://www.dobreprogramy.pl/Volume2,Program,Windows,38701.html).




![desk](https://raw.githubusercontent.com/djfoxer/djfoxer.github.io/master/_img/2010-4-1-_198_/g_-_608x405_-_-_17467x20161215212909_0.png)

