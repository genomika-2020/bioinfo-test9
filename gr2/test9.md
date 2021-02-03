### bioinfo 2020/2021 gr2 (test9)  

Proszę w katalogu domowym na swoim koncie utworzyć katalog `test9_imię_nazwisko`. 
Odpowiedzi do zadań proszę wpisywać do pliku `odpowiedzi.txt`.   
W pierwszej linii tego pliku proszę wpisać swoje imię i nazwisko.   
Oprócz wyników proszę w ramach odpowiedzi opisywać krótko, jak Państwo do wyniku doszli (program, polecenie, tok myślenia).   
Wszystkie potrzebne do wykonania zadań pliki znajdują się w katalogu `/dane/test9`.
***
***

***SRP*** (*ang. signal recognition particle*) to kompleks białka i RNA, który rozpoznaje i 
kieruje do siateczki śródplazmatycznej nowo syntetyzowane polipeptydy, jeśli zawierają one sekwencję sygnałową. 
Białka te mogą później zostać wydzielone poza komórkę, pozostać w błonie, lub też zostać 
skierowane do niektórych organelli (np. aparatu Golgiego).
***
#### Zad1    
U człowieka jednym z białek wchodzących w skład kompleksu SRP jest białko kodowane przez gen **SRP54**.

1. Jaka jest lokalizacja tego genu (chromosom, początek, koniec, nić)? (0.5 pkt)
2. Jaka będzie długość białka powstającego z translacji transkryptu **MANE Select** 
   (to transkrypt, jaki eksperci z NCBI oraz EMBL-EBI uznali, jako
   reprezentacyjny, mający najwyższe znaczenie biologiczne dla danego genu)? (0.5 pkt)
3. Jakie domeny białkowe wchodzą w skład białka powstającego z tego transkryptu (według klasyfikacji **SuperFamily**)? (0.5 pkt)
4. Ile wariantów genetycznych prowadzących do skrócenia białka powstającego z tego transkryptu (***ang PTV, protein truncating variants***) jest znanych (według Ensembl)? (1 pkt)
5. Jaka jest częstość wariantu **rs753087160** w populacji afrykańskiej (według gnomAD)? (0.5 pkt)  
***
#### Zad2  
Aby nowo powstający polipeptyd został rozpoznany i związany przez SRP, musi mieć na N-końcu sekwencję sygnałową. 
1. Proszę uzyskać listę ludzkich genów, dla których program *SignalP* przewiduje obecność takiej sekwencji 
   (program używa dwóch różnych algorytmów no-TM oraz TM).
**Uwaga**: dane te są dostępne w Ensembl - nie trzeba więc samemu uruchamiać programu (i proszę tego nie robić - przynajmniej podczas tego testu)!
Sekwencje sygnałowe w Ensembl określane są jako **Cleavage site (Signalp)** 
Analizę proszę zawęzić do genów kodujących białka i dla których eksperci wybrali transkrypt **MANE Select**. 
Do listy proszę dodać informację o ID genu, położeniu początku i końca sekwencji sygnałowej. Uzyskaną listę proszę zapisać w pliku `zad2.txt`.
(2pkt)
2. Dla ilu genów program SignalP przewidział obecność sekwencji sygnałowej (dodana adnotacja SignalP-TM albo SignalP-noTM)? (0.5 pkt) 
3. Czy sekwencja sygnałowa zawsze zaczyna się od pierwszego aminokwasu? (0.5 pkt)
4. Ile aminokwasów ma najdłuższa zidentyfikowana sekwencja sygnałowa? (1 pkt)

**Uwaga**: Jeśli nie uzyskali Państwo pliku `zad2.txt`, to podpunkty 2-4 można wykonać analizując plik `/dene/test9/zad2-dm.txt`.
Proszę wtedy w odpowiedziach zaznaczyć, że analizowali Państwo ten plik.
***

#### Zad3   
Jeśli białko ma być zakotwiczone w błonie, to oprócz sygnału kierującego go do ER (na N-końcu),
jego sekwencja powinna zawierać też sygnał "stop transfer" - odcinek około 20 hydrofobowych aminokwasów. 
W pliku `zad3.fasta` znajdują się sekwencje białek *Drosophila melanogaster*, dla których program SignalP 
przewidział obecność sekwencji sygnałowej.
W opisie każdej sekwencji znajduje się jej identyfikator Ensembl.
 Proszę napisać skrypt, 
który wyszuka, które z nich mogą zawierać sygnał "stop transfer", według następującego algorytmu
(na pewno niedoskonałego, a może nawet całkiem złego):
* sygnał taki powinien zawierać nieprzerwany ciąg co najmniej 18 hydrofobowych aminokwasów [symbole: G, A, V, L, I, P, M, W, F]  
* sygnał "stop transfer" powinien być położony co najmniej 20 aminokwasów za początkiem i 20 aminokwasów od końca białka.  
Skrypt powinien do pliku `zad3.txt` wypisać identyfikatory genów, dla których znaleziono potencjalne sygnały "stop transfer".

Podpowiedzi:
Aby wyszukać ciąg co najmniej 5 takich samych znaków (tutaj a) w pliku `plik.txt` można zastosować jedno z następujących poleceń:
```bash
grep -E 'a{5,}' plik.txt  
grep 'a\{5,\}' plik.txt
```
Aby wyciąć tekst od znaku 5 do końca linii, można zastosować:
```bash
cut -c5- plik.txt
```
Aby przyciąć linie z dwóch stron można użyć:
```bash
cut -c5- plik.txt | rev | cut -c5- | rev
```
Proszę pomyśleć nad zmianą formatu pliku wejściowego, tak aby zadanie nie było zbyt trudne (np. `fasta_formatter`?). 
Proszę pamiętać, że ciąg taki mógł ulec podzieleniu między kolejnymi liniami.
Proszę zapisać skrypt pod nazwą `zad3.sh`.   
Punktacja: za napisanie w pełni działającego skryptu i uzyskanie pliku wynikowego: 5 pkt.
***

#### Zad4  
1. Proszę zaproponować wyrażenie filtrujące (dla programu SnpSift) dla przypadku rodziny (rodzice i dziecko), 
gdy szukamy mutacji powodującej chorobę dziedziczącą się autosomalnie i recesywnie.
Wiemy, że dziecko jest chore i obydwoje rodzice są nosicielami. Proszę przetestować na pliku `/dane/family.vcf.gz`. Plik jest duży i skompresowany.
Proszę go nie kopiować na swoje konto, tylko podać pełną ścieżkę dostępu do pliku, proszę także zastosować `zcat`:  
   ```bash
   ### podgląd pliku
   zcat plik.vcf.gz | less
   
   ### filtrowanie:  
   zcat plik.vcf.gz | SnpSift filter 'wyrażenie filtrujące' > plik-wynikowy
   ```
   
Oznaczenia genotypów: `M` - matka, `F` - ojciec, `D` - córka.  
Wynik proszę zapisać jako `zad4.vcf` (2 pkt).  
2. Ile wariantów pozostało w wynikowym pliku? (0.5 pkt)
***

#### Zad5
Co to jest element *Alu*? Jaki jest jego związek z kompleksem **SRP**? (0.5 pkt)

***
***
KONIEC. Proszę upewnić się, że następujące pliki znajdują się w katalogu `test9_imie_nazwisko`:
* odpowiedzi.txt 
* zad2.txt
* zad3.sh
* zad3.txt
* zad4.vcf 

