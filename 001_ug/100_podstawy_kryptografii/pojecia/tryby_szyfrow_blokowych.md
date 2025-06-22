# Tryby szyfrów blokowych

## Szyfry blokowe 
- szyfry symetryczne operujące na blokach danych o ustalonym rozmiarze.
- **Działają w rundach**: w każdej rundzie dane są poddawane kolejnym operacjom (dodanie klucza, podstawienie bitów/bajtów, permutacje, itp.).
- Po zakończeniu określonej liczby rund **otrzymujemy zaszyfrowany blok**.
- Ten sam szyfr (wraz z kluczem) można zastosować w różnych trybach pracy (ECB, CBC, OFB itp.), aby przetwarzać większe wiadomości niż pojedynczy blok.

## Tryby szyfrowania blokowego  

### ECB (Electronic Code Book)
- każdy blok mj szyfrowany niezależnie: `cj = Enc(k, mj)`.  
- zalety: prostota, równoległość
- wady: deterministyczność, wykrywalność powtarzających się bloków.  

### CBC (Cipher Block Chaining)
- `cj = Enc(k, mj ⊕ cj−1)`, `c0 = IV`.  
- Zalety:
    - jeśli F jest permutacją pseudolosową, a wektor początkowy jest losowy, to szyfr jest bezpieczny na atak z wybranym tekstem jawnym
- Wady: 
    - przetwarzanie musi być sekwencyjne, nie ma szansy na wykorzystanie ew. równoległości obliczeń
    - błąd w jednym bicie kryptogramu powoduje błąd w dwóch odszyfrowanych blokach

### OFB (Output Feedback)
- strumień rj generowany: `r0 = IV`, `rj = Enc(k, rj−1)`.
- `mj ⊕ rj = cj -> cj ⊕ rj = mj`
- Zalety:
    - błędy w szyfrogramie nie propagują się wcale
    - ciąg rj można przygotować przed otrzymaniem szyfrogramu
    - jeśli F jest funkcją pseudolosową, to szyfr jest bezpieczny na atak z wybranym tekstem jawnym
    - pod warunkiem, że wektor początkowy jest losowy
    - F nie musi być permutacją
- Wady:
    - nie można wykorzystać przetwarzania współbieżnego

### CFB (Cipher Feedback)
- `cj = mj ⊕ Enc(k, c{j−1})`, `c0 = IV`.  
- sekwencyjne przetwarzanie, błąd propaguje się na dwa bloki.  

### CTR (Counter)
- `rj = Enc(k, ctr + j)`, gdzie `ctr = IV`, licznik inkrementowany.  
- rejestr jest licznikiem, umożliwia działanie współbieżne
- można szyfrować niezależne fragmenty