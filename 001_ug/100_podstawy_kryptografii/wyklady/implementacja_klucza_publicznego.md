# Kryptografia klucza publicznego. Implementacja idei

## Teoria grup  
- **Definicja grupy (przemiennej):** zbiór G z działaniem •, takie że:  
  - **jedynka** e: e • a = a • e = a  
  - **łączność**: a • (b • c) = (a • b) • c  
  - **odwrotność**: ∀ a ∃ a⁻¹: a • a⁻¹ = e  
  - **przemienność**: a • b = b • a  
- **Rząd grupy**: |G| (liczba elementów).  
- **Przykłady:**  
  - (ℤ, +) — nieskończona grupa addytywna  
  - (ℤₙ, + mod n) — rząd = n  
  - (ℤₚ*, · mod p) dla p pierwszego — rząd = p–1  
  - grupa multiplikatywna ℤₙ* = {a mod n | gcd(a,n)=1}, rząd = φ(n)

- **Potęgowanie w grupie**
    - Definicja: dla a ∈ G i n ∈ ℕ:  `aⁿ = a • a • … • a` (n razy)
- **Twierdzenie:** a^{|G|} = e  
    - Wynika, że aʲ = aˣ mod |G| w sensie grupowym. Jeśli gcd(j,|G|)=1, to funkcja j ↦ aʲ jest bijekcją i ma odwrót g(a)=aᶦ, gdzie j·i≡1 mod |G|.

## Małe twierdzenie Fermata  
- Jeżeli p jest liczbą pierwszą i p ∤ a, to  

a^{p–1} ≡ 1 mod p

- Dowód: (ℤₚ*, ·) jest grupą rzędu p–1.  
- **Przykład:** 2^{10} ≡ 1 mod 11 ⇒ 2^{123456789} ≡ 2^{9} ≡ 6 mod 11.  
- **Test pierwszości:** sprawdź czy a^{n–1}≡1 mod n dla kilku a; wyjątki to liczby pseudopierwsze (np. 561).

## Funkcja Eulera φ  
- φ(n) = |{ a ∈ {1…n–1} | gcd(a,n)=1 }|  
- Dla n = p prime: φ(p)=p–1.  
- Dla n = pᵏ: φ(pᵏ)=pᵏ – p^{k–1} = (1–1/p)·pᵏ.  
- Ogólnie:  
φ(n) = n · ∏_{q|n} (1 – 1/q)

- Dla n=p·q (p≠q): φ(n)=(p–1)(q–1).

## Twierdzenie Eulera  
- Jeżeli gcd(a,n)=1, to  

a^{φ(n)} ≡ 1 mod n

- Małe tw. Fermata to przypadek n = p.  
- Wniosek: aˣ = aʸ mod n, gdy x≡y mod φ(n).

## Problem rozkładu na czynniki  
- **Gra**: Tadeusz losuje p, q; Ewa dostaje N=p·q i próbuje znaleźć dowolny niespełny rozkład.  
- **Trudność**: brak algorytmu wielomianowego w |N|.  
- Hipoteza: faktoryzacja dużych liczb półpierwszych jest zadaniem trudnym.

## RSA  
- Wybieramy duże p,q (≥500 bitów), N=p·q, φ(N)=(p–1)(q–1).  
- Losujemy e ∈ ℤₙ*; obliczamy d: e·d≡1 mod φ(N) (alg. Euklidesa).  
- Klucz publiczny: (N,e), prywatny: (N,d).  
- Szyfrowanie:  

c = mᵉ mod N

- Deszyfracja:  

m = cᵈ mod N

- Uzasadnienie:  

(mᵉ)ᵈ = m^{e·d} ≡ m^{1 + k·φ(N)} ≡ m·(m^{φ(N)})ᵏ ≡ m mod N


## Złożoność RSA vs łamanie  
| n-bitów | generacja ≈O(n³) | faktoryzacja ≈exp(2√n) |  
|:-------:|:---------------:|:--------------------:|  
|  1024   |    ~10⁹ ops     |    ~10³⁰ ops         |  

## Randomizacja RSA (PKCS#1 v1.5)  
- RSA deterministyczne ⇒ podatne na ataki z wybranym kryptogramem.  
- PKCS#1 v1.5: przed szyfrowaniem dodaje się co najmniej 11 bajtów wypełnienia, z trzema stałymi i resztą losową. Po odszyfrowaniu odrzuca nieprawidłowe wzorce.

## Grupy cykliczne i generatory  
- **Podgrupa** generowana przez g: ⟨g⟩={e, g, g²,…, g^{r–1}}, gdzie r=rząd g.  
- **Generator**: g jest generatorem G jeśli ⟨g⟩=G, czyli r=rząd G.  
- Grupa cykliczna ma przynajmniej jeden generator (może być ich wiele).

## Pierwiastki pierwotne mod p  
- ℤₚ* jest cykliczne rzędu p–1; liczba generatorów = φ(p–1).  
- Test na pierwiastek pierwotny g: dla każdej dzielącej p–1 liczby q sprawdź g^{(p–1)/q}≠1 mod p.  
- **Przykład:** p=601 ⇒ p–1=600, dzielniki pierwsze 2,3,5.  
- 7^{600/2}=7^{300}≠1, 7^{600/3}≠1, 7^{600/5}≠1 ⇒ 7 jest generatorem ℤ₆₀₁*.

## Logarytm dyskretny  
- Dla grupy cyklicznej G z generatorem g i h∈G istnieje x: gˣ=h.  
- Problem: znając (G,g,h), trudno znaleźć x (gdy |G| duże).  
- Podstawa systemów ElGamal i DH.

## „Wymiana” klucza wg Diffie–Hellmana  
- Alicja i Bob uzgadniają G, generator g, wybierają losowe a,b∈[1…p–1].  
- Publikują gᵃ mod p, gᵇ mod p.  
- Każdy oblicza wspólny sekret: (gᵇ)ᵃ = (gᵃ)ᵇ = g^{a·b} mod p.  
- Problem DH: obliczyć g^{a·b} znając gᵃ, gᵇ.

## Problem Diffie–Hellmana (decyzyjny)  
- Mając gᵃ, gᵇ, h ∈ G — sprawdzić, czy h = g^{a·b}.  
- Rozwiązanie logarytmu dyskretnego ⇒ rozwiązanie problemu DH.  
- Odwrotne implikacje: nie zawsze wiadomo.

## Szyfr ElGamal  
- Publiczny klucz Boba: (p, g, β = gᵇ mod p). Prywatny: b.  
- Szyfrowanie m<p:  
1. wybierz y losowo,  
2. r = gʸ mod p,  
3. t = βʸ·m mod p,  
4. szyfrogram = (r, t).  
- Deszyfrowanie przez Boba:  

m = t · r^{–b} mod p

- Uzasadnienie:  

t·r^{–b} = (g^{b·y}·m) · (gʸ)^{–b} = m mod p


## Własności ElGamal  
- Złamanie ⇒ rozwiązanie obliczeniowego DH (DH-hard).  
- ElGamal jest nienazastawne (IND-CPA) dzięki losowości y.  
- **Uwaga:** kluczy publicznego i prywatnego nie można zamienić rolami (jak w RSA).

## Porównanie ElGamal z RSA  
- ElGamal wymaga grupy cyklicznej i generatora — raz ustalone, można wielokrotnie używać.  
- RSA wymaga nowych p,q dla każdego klucza.  
- ElGamal jest z definicji niedeterministyczny (losowy), co zwiększa bezpieczeństwo.

## Atak z wybranym kryptogramem  
- **RSA** (bez paddingu) jest podatne:  
- Mariola prosi o odszyfrowanie (rᵉ·c mod N), wynik = r·m. Da się łatwo odtworzyć m.  
- **ElGamal** także podatne:  
- Mariola modyfikuje szyfrogram (gʸ, βʸ·m·r), prosi o odszyfrowanie — otrzymuje m·r.  
- **Obrona:** stosować paddingy i schematy odporne na CCA (schematy ElGamal‐CCA).

