### bioinfo 2020/2021 gr1 (test10)  

Proszę w katalogu domowym na swoim koncie utworzyć katalog `test10_imię_nazwisko`. 
Odpowiedzi do zadań proszę wpisywać do pliku `odpowiedzi.txt`.  
W pierwszej linii tego pliku proszę wpisać swoje imię i nazwisko.   
Oprócz wyników proszę w ramach odpowiedzi opisywać krótko, jak Państwo do wyniku doszli (program, polecenie, tok myślenia).  
 Wszystkie potrzebne do wykonania zadań pliki znajdują się w katalogu `/dane/test10`. Proszę **nie kopiować** tego katalogu na swoje konto: niektóre pliki są bardzo duże! 
***
***

#### zad1
W pliku `/dane/test10/zad1.fa` znajduje się pewna sekwencja. 
1. Jaka jest jej długość? (0.5 pkt)
2. Czy jest to sekwencja białkowa, czy nukleotydowa? (0.5 pkt)
3. Ile razy w sekwencji pojawia się `A` (pomocna może być komenda `grep -o`)  (1 pkt)
4. Co to za sekwencja? (organizm, gen) (1 pkt)
***
   
### zad2
Proszę znaleźć następujące informacje o ludzkim genie ***ACE2*** :
1. Położenie (chromosom, początek, koniec, nić) (0.5 pkt)  
2. Ilość transkryptów kodujących białko (0.5 pkt) 
3. Funkcję molekularną, jaka pełni kodowane przez ten gen białko (0.5 pkt) 
4. ID genu, kodującego ortologiczne białko u szympansa. 
   W ilu pozycjach aminokwasowych różnią się te białka? (1 pkt)  
5. Jaki jest związek genów/białek analizowanych w Zad1 i Zad2? (0.5 pkt)   
***
   

Wiele grup badawczych poszukuje związku pomiędzy zmiennością genetyczną człowieka (wariantami genetycznymi) a podatnością na zakażenie 
wirusem SARS-CoV-2 lub też wpływem wariantów genetycznych na przebieg choroby COVID-19. 
Dane z wielu ośrodków są zbierane i analizowane w ramach organizacji [*The COVID-19 Host Genetics Initiative*](https://www.covid19hg.org/).
Kolejne trzy zadania będą dotyczyły wyników z najnowszej rundy analiz. Sprawdzą Państwo,
czy znaleziono związek wariantów genetycznych położonych w obrębie sekwencji kodujących białek 
głównego układu zgodności tkankowej (ang. ***M**ajor* ***H**istocompatibility* ***C**omplex*) z ostrym przebiegiem choroby (niewydolnością oddechową).

### Zad3.
U człowieka region głównego układu zgodności tkankowej jest położony na chromosomie 6 (region *HLA*) i obejmuje około 4 mln pz. 
W jego obrębie leży około 140 genów kodujących białka. 
Wiele z nich pełni ważne funkcje w odpowiedzi immunologicznej.  
W pliku `/dane/test10/zad3.txt` znajdą Państwo nazwy kilkunastu genów z tego regionu, związanych z prezentacją antygenów (geny *HLA*) oraz regulacją odpowiedzi immunologicznej (*MICA*). 

1. Proszę uzyskać listę z położeniem wszystkich odcinków kodujących białko (*Genomic coding*) dla tych genów. Podpowiedź: **Structures**.
Proszę, aby lista zawierała nazwę genu, chromosom, położenie początku i końca tych odcinków. Listę proszę zapisać pod nazwą `zad3.tab`. (2 pkt)
2. Proszę z listy usunąć linię nagłówka oraz linie z brakującymi danymi (1 pkt). Odfiltrowany plik proszę zapisać pod nazwą `zad3-filtered.tab`.

### Zad4
W pliku `/dane/test10/COVID19_HGI_B2_ALL_leave_UKBB_23andme_20210107.txt.gz` 
znajdują się wyniki ostatnich analiz *The COVID-19 Host Genetics Initiative*.   
**Uwaga**: Plik jest duży i skompresowany - proszę go nie kopiować na swoje konto i nie rozpakowywać!!!
Dla każdego analizowanego wariantu pokazany jest wynik testu statystycznego
(współczynnik beta oraz wartość p-value), mówiący o tym, czy dany wariant jest związany z ostrym przebiegiem infekcji.
Dane są ułożone w następujący sposób:   
  * kol1: nazwa chromosomu (w konwencji 1-22, X)  
* kol2: położenie wariantu na chromosomie   
* kol3: allel ref  
* kol4: allel alt (dla niego podany jest współczynnik beta)  
* kol7: współczynnik beta (efekt allelu, zwiększenie lub zmniejszenie ryzyka ostrego przebiegu choroby)  
* kol9: wartość *p* (błąd pierwszego rodzaju, im niższy, tym większa szansa, że związek wariantu z chorobą nie jest wynikiem przypadku)  
* kol13: identyfikator wariantu z bazy dbSNP (ostatnia kolumna)   
Pierwsza linia zawiera nagłówek i zaczyna się od znaku `#`.   
     

Państwa zadaniem będzie napisanie skryptu `zad4.sh`, który z pliku `/dane/test10/COVID19_HGI_B2_ALL_leave_UKBB_23andme_20210107.txt.gz` wytnie 
i (zapisze do nowego pliku `zad4.txt`) informacje o wariantach (całe linie)
leżących w obrębie sekwencji kodujących genów z zadania3 (Potrzebny będzie plik `zad3-filtered.tab` z poprzedniego zadania. 
Jeśli go Państwo nie uzyskali - proszę pracować z plikiem `/dane/test10/filtered.txt` i zaznaczyć to w odpowiedziach).     
Zadanie należy wykonać z wykorzystaniem programu `tabix`, pomocny może być także program `zcat`. 
Obydwa programy umożliwiają pracę na skompresowanych danych.
Program `tabix` wymaga dodatkowo, aby skompresowany plik był zindeksowany (w tym samym katalogu musi być obecny plik `COVID19_HGI_B2_ALL_leave_UKBB_23andme_20210107.txt.gz.tbi`).   
Przykładowy sposób użycia:
```bash
### Oglądanie zawartości pliku:
zcat /dane/test10/COVID19_HGI_B2_ALL_leave_UKBB_23andme_20210107.txt.gz | less

### Wyszukiwanie wzorca:
zcat /dane/test10/COVID19_HGI_B2_ALL_leave_UKBB_23andme_20210107.txt.gz | grep 'wzorzec'

### Wyszukanie linii z wariantami z chromosomu 1 położonych pomiędzy 8000000 i 8020000 nukleotydem (włącznie):
tabix  /dane/test10/COVID19_HGI_B2_ALL_leave_UKBB_23andme_20210107.txt.gz 1:8000000-8020000

```
Przed rozpoczęciem pracy nad skryptem proszę wpisać powyższe komendy, pooglądać wyniki, tak aby zorientować się, jak obydwa programy działają.  
Punktacja: za działający skrypt i uzyskanie poprawnego pliku `zad4.txt`: 5 pkt   

### Zad5
1. Który spośród wariantów leżących wewnątrz sekwencji kodujących analizowanych
   genów ma najniższą wartość *p* (kolumna 9). 
   Czy wartość ta jest niższa niż przyjmowany w tego typu badaniach próg istotności *p=5e-08*? 
   Proszę podać identyfikator tego wariantu (rsID, kolumna13). (1.5 pkt)
   **Uwaga**: Wartości błędu pierwszego rodzaju *p* są podane w notacji naukowej (np. 8.678e-11). 
   Aby posortować prawidłowo liczby w tej notacji zamiast zwykłego (poznanego przez Państwa) polecenia `sort/sort -n` należy użyć
  `LC_ALL=C sort -g`. Można dodawać pozostałe, poznane przez Państwa opcje programu sort (np. `-k, -r`). 
   Jeśli nie uzyskali Państwo pliku `zad4.txt` proszę tylko napisać odpowiednią komendę.  
   
