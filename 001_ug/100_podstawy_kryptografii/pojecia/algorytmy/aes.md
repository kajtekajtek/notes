# AES (Advanced Encryption Standard)
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