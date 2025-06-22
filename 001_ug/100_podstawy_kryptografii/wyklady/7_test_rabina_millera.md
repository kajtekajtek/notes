# Test Rabina-Millera

## Szukanie liczb pierwszych  
- **Algorytm „naiwnego sprawdzania”**  
  - Losujemy ciąg n bitów = duża liczba k.  
  - Sprawdzamy, czy k jest pierwsza; jeśli nie – powtórka.  
- **Złożoność**  
    - liczba liczb pierwszych n-bitowych `>= C/n` dla pewnej stałej C
    - a więc średnio n iteracji starcza do znalezienia l. pierwszej
    - problem testowania pierwszości liczby
    - oczywiście nie poprzez próbę rozkładu, ten problem oceniamy jako trudny
    - stosowane w praktyce algorytmy mogą przyjąć, że liczba jest pierwsza nawet jeśli taka nie jest (zaniedbywalne prawdopod. błędu)

## Test pierwszości według Fermata  
- **Małe twierdzenie Fermata:**  
    - Jeśli n jest pierwsza i NWD(a,n)=1, to `a^{n–1} = 1 mod n`

- **Procedura:**  
1. Wybieramy a ∈ [2…n–1], obliczamy NWD(a,n).  
2. Jeśli NWD(a,n)>1 ⇒ n złożona.  
3. Obliczamy a^{n–1} mod n:  
   - Jeśli ≠1 ⇒ n złożona.  
   - Jeśli =1 ⇒ n “pseudopierwsza” względem a.  
- **Uwagi:**  
    - Liczby Carmichaela spełniają Fermata dla każdego a, mimo że są złożone.  
    - Przy m losowych a prawdopodobieństwo, że złożona n przejdzie wszystkie testy ≤ 2^{-m}·log n.

## Test Millera–Rabina  
- **Idea w rozkładzie:**  
    - Jeżeli `x² = y² mod n`, ale `x ≠ ±y` (różne pierwiastki), to NWD(x–y, n) ujawnia nie-trywialny dzielnik n.  
- **Schemat:**  
1. Zapisz `n–1 = m·2ᵏ`, gdzie k > 0, czyli m j. nieparzyste.  
2. Wybierz bazę a ∈ [2…n–2], oblicz b₀ ≡ aᵐ mod n.  
3. Dla i=0…k–1:  
   - b_{i+1} ≡ b_i² mod n  
   - Jeśli b_{i} ≡ 1 mod n i b_{i–1} ≠ ±1 mod n ⇒ wyłapujemy rozkład (NWD(b_{i–1}–1, n)).  
4. Jeśli b₀ ≠ 1 i żadne przejście nie daje –1 przed końcem ⇒ n złożona.  
5. W przeciwnym razie n prawdopodobnie pierwsza.  
- **Przykład (n=561):**  
    - 561–1 = 35·2⁴  
    - Dla a=2:  
    ```
    b₀ = 2³⁵ ≡ 263  
    b₁ = 263² ≡ 166  
    b₂ = 166² ≡  67  
    b₃ =  67² ≡   1  
    ```  
    - NWD(67–1,561)=33 ⇒ 561=33·17.

## Generowanie liczb pierwszych  
- **Podejście probabilistyczne:**  
1. Losujemy kandydat k o n bitach.  
2. Sprawdzamy testy Rabina–Millera dla kilku baz (np. 2,3,5,7…).  
3. Jeśli żaden test nie wykrył złożoności – uznajemy k za pierwszą.  
- **Pewność i złożoność:**  
- Jeśli n złożona, to mniej niż ¼ baz jest „świadkiem pierwszości” ⇒ po t niezależnych testach błąd ≤ (1/4)ᵗ.  
- Złożoność całkowita ≈ O(k³) dla n-bitowego n i t = O(1) testów.

## Liczby silnie pierwsze  
- **Definicja:** p jest silnie pierwsza, jeśli:  
    - p jest pierwsza,  
    - (p–1)/2 także jest pierwsza.  
- **Zastosowanie:** wykorzystywane w generowaniu parametrów RSA i DH, by zabezpieczyć przed niektórymi atakami na grupę ℤₚ*.  
- **Generowanie:**  
    1. Szukamy pierwszej q ≈ n/2 bitów.  
    2. Testujemy p = 2·q + 1 na pierwszość.  
    3. Jeśli nie – powtarzamy z kolejnym q.  
- **Słabsza wersja:**  
    - Wystarczy, że (p–1)/2 ma duży dzielnik pierwszorzędowy, a nie jest sam pierwsza — uproszczenie przy dużych parametrach.