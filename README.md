### bioinfo 2020/2021 gr2 (test9)  

***SRP*** (*ang. signal recognition particle*) to kompleks białka i RNA, który rozpoznaje i 
kieruje do siateczki śródplazmatycznej nowo syntetyzowane polipeptydy, jeśli zawierają one sekwencję sygnałową. 
Białka te mogą później zostać wydzielone poza komórkę, pozostać w błonie, lub też zostać 
skierowane do niektórych organelli (np. aparatu Golgiego).

#### Zad1    
U człowieka jednym z białek wchodzących w skład kompleksu SRP jest białko kodowane przez gen **SRP54**.

1. Jaka jest lokalizacja tego genu (chromosom, początek, koniec, nić)? (0.5 pkt)

2. Jaka będzie długość białka powstającego z translacji transktyptu **MANE Select** 
   (to transkrypt, jaki eksperci z NCBI oraz EMBL-EBI uznali, jako
   reprezentacyjny, mający najwyższe znaczenie biologiczne dla danego genu)? (0.5 pkt)
   
3. Jakie domeny białkowe wchodzą w skład białka powstającego z tego transkryptu (według klasyfikacji **SuperFamily**)? (0.5 pkt)
4. Ile wariantów genetycznych prowadzących do skrócenia białka powstającego z tego transkryptu (**ang PTV, protein truncating variants**) jest znanych (według Ensembl)? (1 pkt)
5. Jaka jest częstość wariantu **rs753087160** w populacji afrykańskiej (według gnomAD)? (0.5 pkt)  

#### Zad2  
Aby nowo powstający polipeptyd został rozpoznany i związany przez SRP, musi mieć na N-końcu sekwencję sygnałową. 
1. Proszę uzyskać listę ludzkich genów, dla których program *SignalP* przewiduje obecność takiej sekwencji. 
**Uwaga**: dane te są dostępne w Ensembl - nie trzeba więc samemu uruchamiać programu (i proszę tego nie robić - przynajmniej podczas tego testu)!
Sekwencje sygnałowe w Ensembl określane są jako **Cleavage site (Signalp)** 
Analizę proszę zawęzić do genów kodujących białka i dla których eksperci wybrali transkrypt **MANE Select**. 
Do listy proszę dodać informację o ID genu, położeniu początku i końca sekwencji sygnałowej. Uzyskaną listę proszę zapisać w pliku **zad2.txt**.
(2pkt)
2. Dla ilu genów program SignalP przewidział obecność sekwencji sygnałowej? (0.5 pkt) 
3. Czy sekwencja sygnałowa zawsze zaczyna się od pierwszego aminokwasu? (0.5 pkt)
4. Ile aminokwasów ma najdłuższa zidentyfikowana sekwencja sygnałowa? (1 pkt)

#### Zad3   
Jeśli białko ma być zakotwiczone w błonie, to oprócz sygnału kierującego go do ER (na N-końcu),
jego sekwencja powinna zawierać też sygnał "stop" - odcinek około 20 hydrofobowych aminokwasów. 
W pliku `zad3.fasta` znajdują się sekwencje białek *Drosophila melanogaster*, dla których program SignalP 
przewidział obecność sekwencji sygnałowej.
W opisie każdej sekwencji znajduje się jej identyfikator Ensembl.
 Proszę napisać skrypt, 
który wyszuka, które z nich mogą zawierać odcinki transmembranowe, według następującego algorytmu
(na pewno niedoskonałego, a może nawet całkiem złego):
* odcinek taki powinien zawierać nieprzerwany ciąg co najmniej 18 hydrofobowych aminokwasów [symbole: G, A, V, L, I, P, M, W, F]  
* odcinek ten powinien być położony co najmniej 20 aminokwasów za początkiem i 20 aminokwasów od końca białka.  
Skrypt powinien do pliku `zad3.txt` wypisać identyfikatory genów, w których zidentyfikowano możliwe odcinki transbłonowe.

Podpowiedź: aby wyszukać ciąg co najmniej 5 takich samych znaków (tutaj a) w pliku `plik.txt` można zastosować jedno z następujących poleceń:
```bash
grep -E 'a{5,}' plik.txt  
grep 'a\{5,\}' plik.txt
```
Proszę pomyśleć nad zmianą formatu pliku wejściowego, tak aby zadanie nie było zbyt trudne (np. `fasta_formatter`?). 
Proszę pamiętać, że ciąg taki mógł ulec podzieleniu między kolejnymi liniami.
Proszę zapisać skrypt pod nazwą `zad3.sh`.   
Punktacja: za napisanie w pełni działającego skryptu i uzyskanie pliku wynikowego: 5pkt.

#### Zad4  
1. Proszę zaproponować wyrażenie filtrujące (dla programu SnpEff) dla przypadku rodziny (rodzice i dziecko), 
gdy szukamy mutacji powodującej chorobę dziedziczącą się autosomalnie i recesywnie.
Wiemy, że dziecko jest chore i obydwoje rodzice są nosicielami. Proszę przetestować na uzyskanym podczas ćwiczeń pliku `razem.vcf`. 
Wynik proszę zapisać jako `zad4.vcf` (1.5 pkt).  
2. Powyższe wyrażenie poradzi sobie tylko z przypadkiem, gdy dokładnie ta sama mutacja znajduje się u obydwóch rodziców. 
   Tymczasem może się zdarzyć, że dwie różne zmiany w obrębie tego samego genu "spotkają się" u dziecka. Proszę napisać w punktach, jak można by takie warianty znaleźć.
   
**Uwaga**: to zadanie polega tylko na pomyśleniu nad problemem i wypisaniu do pliku swoich pomysłów (plik `zad4.txt`) (1.5 pkt).  





