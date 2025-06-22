# Szyfry blokowe

## Funkcje pseudolosowe  
- Oznaczenie: \[n\] = zbiór ciągów bitów długości n, operacja ⊕ = dodawanie bitów mod 2.  
- Funkcja `F: [n] × [n] → [n]`, efektywna w czasie wielomianowym (PPT), klucz k ∈ \[n\].  
- F jest **pseudolosowa**, jeśli przeciwnik w zasobach PPT nie odróżni F(k,·) od prawdziwej losowej funkcji f, nawet znając część jej wartości.  
- Funkcje pierwszego typu (z zakresem ≤2ⁿ) jest 2ⁿ, drugiego typu (permutacje) jest (2ⁿ)!.  
- Sam zapis f: \[n\]→\[n\] wymaga wykładniczych zasobów, więc PPT-owy F jest cenny.

## Permutacje pseudolosowe  
- `F: [n]×[n]→[n]` jest **permutacją z kluczem**, jeśli dla każdego k, F(k,·) jest bijekcją.  
- F jest **pseudolosową permutacją**, jeśli F(k,·) i jej odwrotność są nieodróżnialne od losowych permutacji.  
- Można wymagać, by i F⁻¹(k,·) była pseudolosowa.

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

## Właściwości trybów blokowych  
- **Bezpieczeństwo:** rośnie z rozmiarem bloku (≥128 bitów dziś).  
- **Odporny na atak z wybranym kryptogramem:** strumieniowe tryby (OFB, CFB, CTR) zapewniają, że lekkie zaburzenie w szyfrogramie daje minimalne zmiany w odszyfrowaniu.  
- **CBC:** błąd w jednym bicie szyfrogramu psuje dwa bloki odszyfrowane (propagacja błędu).  
- **ECB:** odradzany ze względu na deterministyczność i powtarzalność wzorców.

## Koncepcje Shannona: konfuzja i dyfuzja
**Konfuzja** – wprowadzenie jak największego „zamieszania” w relacji między kluczem a szyfrogramem, aby przeciwnik nie mógł wnioskować o kluczu, znając tekst jawny i szyfrogram.
- W praktyce konfuzja często sprowadza się do stosowania **podstawień** (ang. substitution), np. przez tablice S-box.
- W teorii można by użyć olbrzymich bijekcji (permutacji) na całym bloku, ale dla dużych bloków (np. 64-bitowych) jest to niepraktyczne (zbyt ogromna liczba możliwych permutacji).

**Dyfuzja** – rozproszenie wpływu każdego bitu tekstu jawnego (lub klucza) na jak największą liczbę bitów szyfrogramu.
- Zmiana jednego bitu na wejściu powinna „rozlać się” po całym bloku wyjściowym.
- W praktyce realizowane to jest m.in. przez przeplatane stosowanie podstawień (S-boxów) oraz permutacji (mieszających bity między sobą).

## Sieci podstawień i permutacji (Substitution-Permutation Network, SPN)
W sieci SPN blok danych wielokrotnie przechodzi przez rundy składające się z:
1. Dodania klucza (operacja $\oplus$) – mieszanie bloków z kluczem rundy.
2. Podstawienia (S-box) – każdy mały fragment (np. 4 lub 8 bitów) przechodzi przez funkcję podstawieniową, która jest bijekcją (aby dekodowanie było możliwe).
3. Permutacji bitów – bity wewnątrz bloku są mieszane, aby zapewnić dyfuzję.

### Właściwości sieci SPN
- Odwracalność
    
    Konieczna do odszyfrowania: wszystkie operacje (dodawanie klucza, S-box, permutacja bitów) muszą być odwracalne.

- Efekt lawiny (ang. avalanche effect)
    - Zmiana choćby jednego bitu wejściowego może skutkować zmianą wielu bitów wyjściowych.
    - W praktyce: w każdym S-boksie zmiana pojedynczego bitu wejścia powinna (w typowym projekcie) zmieniać co najmniej dwa bity wyjścia.
    - Zmienione bity rozchodzą się dalej przez permutacje i kolejne S-boksy.
    - Wymagana jest dostateczna liczba rund, by uzyskać odpowiednią „głębię” dyfuzji.

###  Przykład (w formie schematycznej)
Runda:
1. Dodaj klucz rundy (XOR z częścią klucza zależną od rundy).
2. Zastosuj S-boksy do małych fragmentów (np. 4- czy 8-bitowych).
3. Permutuj bity w obrębie bloku, aby każde wyjście S-boxa trafiło w inne miejsce w kolejnej rundzie.

Powtórz powyższe kroki w kilku (kilkunastu) rundach.
*Ostatni krok*: często bywa dodatkowe dodanie klucza (lub inna drobna operacja), aby ostatecznie zaszyfrować blok.

### Sieci Feistela
Konstrukcja szyfru, w której blok (o długości 2n) dzielony jest na dwie części: **L** i **R** (po **n bitów**).

Runda sieci Feistela: 
- $F(k, \langle L, R \rangle) = \langle R, L \oplus f(k, R)\rangle$

gdzie f to dowolna funkcja (nie musi być bijekcją!).

Główna zaleta: odwracalność – wystarczy zastosować tę samą funkcję F dwa razy, by uzyskać pierwotny blok (lub identyczną konstrukcję w odwrotnym porządku).

### Szyfr Feistela w praktyce
Dany blok ($L_0, R_0$) przechodzi przez kolejne rundy:
- $L_i = R_{i-1}, R_i = L_{i-1}\oplus f(k_i, R_{i-1})$

gdzie $k_i$ to klucze rundowe (zależne od klucza głównego).

Po ostatniej rundzie można (lub nie) zamienić miejscami $L_n$ i $R_n$​ – zależy to od definicji szyfru.

**Odszyfrowywanie** wygląda podobnie, ale używa kluczy w odwrotnej kolejności.

### Funkcja f
- Może być praktycznie dowolna, byle była dobrze mieszająca. 
- Jest to często miejsce, gdzie umieszcza się S-boksy, permutacje, rozszerzenia bitów itp. 
- Sieci Feistela są bardzo popularne m.in. w DES i wielu innych szyfrach.

## Szyfr DES (Data Encryption Standard)
Zaprojektowany w IBM (pod nazwą „Lucifer” – wstępna wersja). Poprawiona wersja opublikowana w 1975, za standard uznany w 1977. Choć formalnie **zdezaktualizowany w roku 2000** (zastąpiony przez AES), **wciąż bywa używany** ze względu na szerokie wdrożenie.

### Główne cechy DES
- Blok 64-bitowy (dane wejściowe/wyjściowe).
- Klucz 56-bitowy (realnie ma 64 bity, ale 8 z nich służy do parzystości).
- 16 rund opartych na sieci Feistela.

### Struktura rundy DES
1. **Początkowa permutacja** (IP) na bloku 64-bitowym.
2. Podział na dwie części po 32 bity: $L_0$ i $R_0$.
3. Każda z 16 rund:
    - $L_i = R_{i-1}$
    - $R_i = L_{i-1}\oplus f(K_i, R_{i-1})$
    - Funkcja f zawiera:
        - Permutację rozszerzającą EE (z 32 bitów do 48).
        - Dodanie klucza rundy (XOR z 48-bitowym kluczem rundy).
        - 8 S-boksów (każdy przyjmuje 6 bitów i zwraca 4 bity).
        - Ostatnią permutację (P) w obrębie 32 bitów.
4. Zamiana (Swap) po 16. rundzie, a następnie końcowa permutacja odwrotna ($IP^{-1}$).

### Generowanie kluczy rundowych
- Klucz 56-bitowy dzielony jest na dwie części (28 + 28).
- W każdej rundzie **obie części są przesuwane** (o 1 lub 2 bity), a następnie z **56 bitów wybieranych jest 48** – to jest klucz rundowy.
- Zasada przesunięć w poszczególnych rundach jest zdefiniowana w standardzie (tabela z wartościami 1 lub 2).

### Bezpieczeństwo i ataki na DES
- Brute force (przeszukiwanie klucza 2^56)
    - Pierwotnie uważano to za trudne (lata 70. i 80.).
    - Pod koniec lat 90. zbudowano urządzenia (tzw. DES Cracker), zdolne do złamania DES w ciągu dni czy nawet godzin, wykorzystując specjalizowany sprzęt lub sieci rozproszone.
- Analiza różnicowa (odkryta oficjalnie w 1990, ale IBM znał ją wcześniej)
    - DES zaprojektowano tak, by był odporny – wymaga zbyt wielu par tekstów do praktycznej realizacji.
- Analiza liniowa (odkryta w 1993)
    - Również trudna w praktycznym zastosowaniu – potrzeba 2^43 tekstów.
- DESX (wzmacnia DES przez dodatkowe operacje XOR na wejściu i wyjściu).
- Podwójne i potrójne szyfrowanie (2DES i 3DES) – rozwiązanie problemu zbyt krótkiego klucza.

**2DES**

Teoretycznie oferuje przestrzeń kluczy 2^112, ale istnieje atak „meet in the middle” złożoności około 2^112 w pamięci i 2^56 w czasie, co ogranicza użyteczność.

**3DES**

Powszechnie stosowana wersja: E(k1, D(k2, E(k1, m))).
- Moc szyfru jest jak 2^112 (bez ataku w stylu 2DES).
- Wsteczna kompatybilność z DES (ustawiając k1 = k2).
- Do niedawna uznawany za bezpieczny, choć wolniejszy od nowocześniejszych szyfrów (np. AES).

## AES (Advanced Encryption Standard)
Ogłoszony przez NIST w 1997 jako następca DES (z powodu krótkiego klucza i rosnącej mocy obliczeniowej).

Wymagania:
- Długość klucza 128, 192 lub 256 bitów.
- Blok 128-bitowy.
- Efektywna implementacja zarówno w urządzeniach o małej mocy obliczeniowej (np. karty inteligentne), jak i w komputerach osobistych/serwerach.

Spośród 15 kandydatów wybrano 5 finalistów: MARS (IBM), RC6 (RSA), Rijndael, Serpent, Twofish.

Ostatecznie w 2000 roku standardem został Rijndael, nazwany po wprowadzeniu do standardu – AES.

### Rijndael (AES)
Sieć podstawień i permutacji:
- Blok 128-bitowy traktowany jako macierz 4×4 bajtów.
- Operacje w rundach:
    - **SubBytes** – ta sama tablica S (S-box) stosowana do każdego bajtu (zapewnia konfuzję).
    - **ShiftRows** – permutacja w wierszach macierzy: przesunięcie bajtów w lewo o różną liczbę pozycji.
    - **MixColumns** – operacja mieszania kolumn, wykonywana w arytmetyce ciała skończonego (dyfuzja).
    - **AddRoundKey** – XOR bajtów macierzy z podrundowym kluczem (kolejna część klucza głównego).

- **Klucz**:
    - Może mieć **długość 128, 192 lub 256 bitów**.
    - Klucz rozwijany jest w tzw. **rundowe klucze** (ang. key schedule) – każdy rundowy klucz także ma postać 4×4 bajtów (lub odpowiednio większą macierz w wersjach AES-192 i AES-256).

- **Odwracalność i bezpieczeństwo**:
    - Wszystkie operacje (w tym MixColumns) są tak zdefiniowane, by dało się łatwo uzyskać funkcję odwrotną.
    - AES uznawany jest za bezpieczny – nie ma praktycznych ataków lepszych niż brute force.