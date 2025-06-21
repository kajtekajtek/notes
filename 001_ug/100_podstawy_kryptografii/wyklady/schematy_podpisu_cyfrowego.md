# Schematy podpisu cyfrowego

## Podpis cyfrowy – podstawy  
- **Cel:**  
  - Przekonać odbiorcę o autentyczności dokumentu, dodatkowo przekonać też stronę trzecią - niezaprzeczalność.
- **W symetrycznej kryptografii:**  
  - Wspólny sekret K, MAC chroni integralność → wiadomość pochodzi od posiadaczy K.  
  - **Brak** niepodważalności: i Alicja i Bolek mogą sporządzić ten sam dokument, sąd nie ma podstaw wierzyć Bolkowi, że autorem jest Alicja a nie Bolek
- **Wymagane cechy podpisu:**  
  - Niemożność fałszerstwa (bez klucza prywatnego).  
  - Niemożność przeniesienia na inny dokument.  
  - Niemożność zmiany podpisanego dokumentu.  
  - Łatwość weryfikacji i identyfikacji osoby podpisującej.

## Podpis cyfrowy w kryptografii symetrycznej  
- **Protokół z zaufanym arbitrem (Tadeusz):**  
  1. Tadeusz zna wszystkie klucze K_A, K_B,…  
  2. Alicja szyfruje dokument M dla Tadeusza: `KA(M)`, z informacją, że adresatem jest Bolek i wysyła do T.  
  3. T odszyfrowuje → ponownie szyfruje dla Bolka: `KB(⟨M,A⟩)` i przekazuje Bolkowi.  
  4. Bolek wierzy Tadeuszowi, że wiadomość jest od Alicji, w razie potrzeby powoła się na Tadeusza, który jest powszechnie szanowany
- **Wady:**  
  - Wymaga zaufanego pośrednika.  
  - Wysokie koszty obliczeniowe i komunikacyjne.  
  - Podpis szkaluje się dla jednego odbiorcy.

## Podpis cyfrowy w kryptografii asymetrycznej  
- Dwie funkcje odwrotne:  
    - F(k_pub, m) → c (szyfrowanie kluczem publicznym)
    - G(k_priv, c) → m (deszyfrowanie kluczem prywatnym)

- **Podpis:** F(k_priv, m), weryfikacja G(k_pub, sig) == m.  
- Klucze nie muszą być zamienne rolami (RSA tak, ElGamal nie).

## Porównanie MAC vs. podpis cyfrowy  

|                  | MAC                       | Podpis cyfrowy           |
|------------------|---------------------------|--------------------------|
| Wspólny klucz    | Wymagany                  | Nie                      |
| Weryfikacja      | Tylko posiadacz klucza    | Każdy z kluczem publicznym |
| Jednokrotność    | Dla każdej sesji trzeba nowy MAC | Raz podpisany → wszyscy widzą |
| Przenoszalność   | MAC nie dowodzi zobowiązania | Podpis wiąże z dokumentem i autorem |

## Algorytm RSA – podpisowanie  

### **Generacja (Alicja):**  
1. Wybiera duże pierwsze p,q → N = p·q, φ(N)=(p–1)(q–1).  
2. Wybiera e,d: e·d≡1 mod φ(N).  
3. Klucze: publiczny (N,e), prywatny (N,d).  

- **Podpis:**  
    - s = mᵈ mod N
    - (wymaga m < N i NWD(m,N)=1)  

### **Weryfikacja (Bolek):**  

m′ = sᵉ mod N

jeśli m′ == m ⇒ podpis OK.  
- **Każdy** z kluczem publicznym może powtórzyć ten proces.

## Słabości RSA jako schematu podpisu  
- **Fałszerstwo egzystencjalne:**  
- Mariola wybiera y, oblicza m = yᵉ mod N, twierdząc że to podpis m.  
- Nie ma sensownej treści, ale jest poprawny podpis.  
- **Fałszerstwo z wybranym tekstem:**  
- Dwa podpisy s₁=m₁ᵈ, s₂=m₂ᵈ ⇒ można podpisać m = m₁·m₂ jako s = s₁·s₂.

## RSA – podpis ślepy (Chaum)  
- **Cel:** Bolek ma podpisać m, którego nie widzi (np. patent).  
- **Algorytm:**  
1. Alicja wybiera losowe k coprime N, wysyła m·kᵉ mod N do B.  
2. Bolek podpisuje: y = (m·kᵉ)ᵈ mod N = mᵈ·k mod N.  
3. Alicja usuwa k: s = y·k⁻¹ mod N → s = mᵈ.  
- Bolek nie wie, co podpisał → wynika, że taki podpis musi być składany wyłącznie przy pomocy dedykowanych kluczy blind-signature.

## Podpis skrótu jako zasada ogólna  

### Dokument jest długi → podpisujemy tylko skrót:  
- h = H(m) (funkcja skrótu)
- s = Sign(k_priv, h)

### **Weryfikacja:** 
- weryfikuje się podpis skrótu i porównuje H(m).  

### **Bezpieczeństwo:**  
- Silna odporność na kolizje (collision resistance).  
- Podpis skrótu jest bezpieczny, jeśli schemat podpisu i H są bezpieczne.

## Funkcje skrótu – atak urodzinowy  
- Prawdopodobieństwo, że w zbiorze r elementów znajdą się dwie o tym samym skrócie ≈ 1 – exp(–r²/2n).  
- Dla n-bitowego wyjścia H, potrzebujemy ≈2^{n/2} prób na kolizję.  
- **Wniosek:** długość wyjścia ≥ 2·bezpieczeństwo (np. 256-bitowy skrót dla 128-bitowego bezpieczeństwa).

## Podpis skrótu w RSA  
- **Podpis:** ⟨m, H(m)ᵈ mod N⟩.  
- **Fałszerstwa:**  
    - Egzystencjalne (łatwe jak wcześniej).  
    - Kolizyjne (łatwo wygenerować dwie wersje o tym samym skrócie).  
- **Uwaga:** bez dowodu formalnego, RSA-hash-then-sign opiera się na sile H i trudności RSA.

## Schemat ElGamal (podpisający)  

### **Generacja (Alicja):**  
1. Wybiera p, generator g, prywatny a < p–1.  
2. Publiczny: β = gᵃ mod p.  

### **Podpis m (<p):**  
1. Losuje k coprime p–1.  
2. r = gᵏ mod p.  
3. s = k⁻¹·(m – a·r) mod (p–1).  
4. Szyfrogram: (r, s).  

### **Weryfikacja (Bolek):**  
- gᵐ ≡ βʳ · rˢ mod p
- **Niedeterministyczny:** różne k → różne podpisy dla tego samego m.

## Schemat ElGamal – losowość i słabość  
- Dwa podpisy na te same m z tym samym k ujawniają a:  
    - `s₁ – s₂ ≡ k⁻¹·(m – a·r) – k⁻¹·(m – a·r) = 0 ⇒ atak`
- Jeśli k jest skompromitowane, można fałszować wszystkie podpisy.

## Digital Signature Algorithm (DSA)  
- Standard FIPS od 1994 r., oparty na discrete log.  
- Podpisywanie: podobne do ElGamal, ale dwa eksponenty i jeden modulo q | p–1.  
- Wymaga silnego generatora grupy rzędu prime q i funkcji skrótu SHA-1/SHA-2.  
- Szybszy niż ElGamal → mniejsze eksponenty, dwie potęgowania zamiast trzech.

## Dlaczego logarytm dyskretny?  
- Wymaga dwóch funkcji wzajemnie odwrotnych:  
    - F(k_pub, m) = sig
    - G(k_priv, sig) = m
- oraz by były commutative w kontekście podpisu vs szyfrowania.  
    - RSA spełnia warunki przez potęgowanie; ElGamal nie pozwala na zamianę ról.  
    - DSA/ElGamal-like schematy projektowane specjalnie pod podpis → nie dają funkcji szyfrującej.