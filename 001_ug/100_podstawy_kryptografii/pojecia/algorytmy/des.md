# Szyfr DES (Data Encryption Standard)
Zaprojektowany w IBM (pod nazwą „Lucifer” – wstępna wersja). Poprawiona wersja opublikowana w 1975, za standard uznany w 1977. Choć formalnie **zdezaktualizowany w roku 2000** (zastąpiony przez AES), **wciąż bywa używany** ze względu na szerokie wdrożenie.

## Główne cechy DES
- Blok 64-bitowy (dane wejściowe/wyjściowe).
- Klucz 56-bitowy (realnie ma 64 bity, ale 8 z nich służy do parzystości).
- 16 rund opartych na sieci Feistela.

## Struktura rundy DES
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

## Generowanie kluczy rundowych
- Klucz 56-bitowy dzielony jest na dwie części (28 + 28).
- W każdej rundzie **obie części są przesuwane** (o 1 lub 2 bity), a następnie z **56 bitów wybieranych jest 48** – to jest klucz rundowy.
- Zasada przesunięć w poszczególnych rundach jest zdefiniowana w standardzie (tabela z wartościami 1 lub 2).

## Bezpieczeństwo i ataki na DES
- Brute force (przeszukiwanie klucza 2^56)
    - Pierwotnie uważano to za trudne (lata 70. i 80.).
    - Pod koniec lat 90. zbudowano urządzenia (tzw. DES Cracker), zdolne do złamania DES w ciągu dni czy nawet godzin, wykorzystując specjalizowany sprzęt lub sieci rozproszone.
- Analiza różnicowa (odkryta oficjalnie w 1990, ale IBM znał ją wcześniej)
    - DES zaprojektowano tak, by był odporny – wymaga zbyt wielu par tekstów do praktycznej realizacji.
- Analiza liniowa (odkryta w 1993)
    - Również trudna w praktycznym zastosowaniu – potrzeba 2^43 tekstów.
- DESX (wzmacnia DES przez dodatkowe operacje XOR na wejściu i wyjściu).
- Podwójne i potrójne szyfrowanie (2DES i 3DES) – rozwiązanie problemu zbyt krótkiego klucza.

## 2DES
Teoretycznie oferuje przestrzeń kluczy 2^112, ale istnieje atak „meet in the middle” złożoności około 2^112 w pamięci i 2^56 w czasie, co ogranicza użyteczność.

## 3DES
Powszechnie stosowana wersja: E(k1, D(k2, E(k1, m))).
- Moc szyfru jest jak 2^112 (bez ataku w stylu 2DES).
- Wsteczna kompatybilność z DES (ustawiając k1 = k2).
- Do niedawna uznawany za bezpieczny, choć wolniejszy od nowocześniejszych szyfrów (np. AES).