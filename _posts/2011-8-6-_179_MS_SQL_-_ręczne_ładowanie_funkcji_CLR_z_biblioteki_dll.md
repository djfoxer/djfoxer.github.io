---
layout:     post
title:      MS SQL - ręczne ładowanie funkcji CLR z biblioteki dll
date:       2011-08-06 15:44:00
summary:    Wpis będzie krótki i treściwy: "jak ręcznie wgrać funkcję CLR do bazy MS SQL, mając bibliotekę dll?" :)Kilka razy zdarzyło mi się, iż musiałem wgrywać funkcje CLR do bazy danych, ale nie było możliwość zrobienia szybkiego deploya z poziomu Visual Studio. Jedynie co mieliśmy do dyspozycji to bibliote...
categories: programowanie
---



Wpis będzie krótki i treściwy: "jak ręcznie wgrać funkcję CLR do bazy MS SQL, mając bibliotekę dll?" :)

Kilka razy zdarzyło mi się, iż musiałem wgrywać funkcje CLR do bazy danych, ale nie było możliwość zrobienia szybkiego deploya z poziomu Visual Studio. Jedynie co mieliśmy do dyspozycji to biblioteka dll z CLR. 

Oto kilka kroków jak wgrać taką dllkę do MS SQL:

1. Przygotowanie bazy pod CLRki:
[code]

USE [master]
GO
GRANT UNSAFE ASSEMBLY TO PUBLIC
USE [NAZWA_BAZY]
GO

EXEC dbo.sp_changedbowner @loginame = N'sa', @map = FALSE
ALTER DATABASE [NAZWA_BAZY] SET TRUSTWORTHY ON

EXEC sp_configure 'show advanced options' , '1';
GO
RECONFIGURE;
GO

[/code]

2. Mając już przygotowaną bazę pod CLRki wrzucamy dllkę:

[code]

CREATE ASSEMBLY [NAMESPACE_DLLKI] FROM 'c:\nasza_bilbioteka.dll' WITH PERMISSION_SET = unsafe 

[/code]

3. Ostatnim krokiem będzie stworzenie CLRek:

[code]

USE [NAZWA_BAZY]
GO

CREATE FUNCTION [dbo].[NAZWA_FUNKCJI_1](@PARAMETR1 TYP,@PARAMETR2 TYP(,..))
RETURNS ZWRACANY_TYP WITH EXECUTE AS CALLER
AS
EXTERNAL NAME [NAMESPACE_DLLKI].[UserDefinedFunctions].[NAZWA_FUNKCJI_2]

[/code]

 *Gdzie:
[NAZWA_BAZY] - nazwa naszej bazy
[NAMESPACE_DLLKI] - Namespace naszej dllki (bierzemy np.z vs)
'c:\nasza_bilbioteka.dll' - ścieżka do biblioteki dll (musimy mieć dostęp)
[NAZWA_FUNKCJI_1] - nazwa funkcji widziana w SQL
[NAZWA_FUNKCJI_2] - nazwa funkcji z dllki
@PARAMETR1 TYP - nazwa parametru wejściowego i jego typ, oczywiście nieobowiązkowe
ZWRACANY_TYP - typ jaki  zwraca CLRka


* 

W taki oto sposób przygotowaliśmy bazę, aby działały w niej funkcje CLR oraz wrzuciliśmy przykładową funckję CLR z bilbioteki dll.

Mam nadzieję, iż wpis komuś się przyda :)



