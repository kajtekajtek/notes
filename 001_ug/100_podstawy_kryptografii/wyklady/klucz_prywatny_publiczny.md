# Kryptografia klucza prywatnego a kryptografia klucza publicznego

## 1. Zarządzanie kluczami prywatnymi  
- **Paradoks kryptografii klucza prywatnego:**  
  - Szyfrowanie symetryczne umożliwia bezpieczne przesłanie tekstu, ale… jak przekazać klucz?  
- **Dlaczego używamy kryptografii klucza publicznego?**  
  1. Klucze publiczne mogą być krótsze niż długie teksty jawne.  
  2. Można je rozpowszechnić niezależnie od czasu i miejsca.  
- **Wymiana klucza symetrycznego (przykład dla n uczestników):**  
  - W prostym modelu każdy z n uczestników musiałby wcześniej bezpośrednio wymienić się z każdym innym kluczem ⇒ n(n–1)/2 par.  
  - Alternatywa: centralne centrum, które trzyma parę kluczy Kᵢ dla każdego użytkownika i rozsyła zaszyfrowane klucze sesyjne:  
    ```
    E(Kᵢ, K_session), E(Kⱼ, K_session)
    ```  
  - Bezpieczeństwo systemu zależy jednak od bezpieczeństwa centrum.

---

## 2. Rewolucja w kryptografii asymetrycznej  
- **Diffie–Hellman (USA, 1976):**  
  - Pierwszy pomysł na kryptografię asymetryczną – system z dwoma kluczami:  
    - **Kₑ** (klucz publiczny) i **K_d** (klucz prywatny)  
    - Dla każdego możliwego komunikatu m:  
      ```  
      Dec(K_d, Enc(Kₑ, m)) = m  
      ```  
  - Znajomość klucza publicznego nie ujawnia klucza prywatnego.  
- **Zastosowania:**  
  1. Szyfrowanie bez wcześniejszej wymiany klucza.  
  2. **Podpis cyfrowy** (niezaprzeczalność).  
  3. Uzgodnienie wspólnego klucza (tzw. “wymiana klucza”).  
- **Implementacja Diffie–Hellmana:**  
  - Jedna procedura służy zarówno do ustalenia wspólnego sekretu, jak i do szyfrowania/podpisu, zależnie od kontekstu.

---

## 3. Kryptografia asymetryczna: szyfrowanie i podpis  
1. **Szyfrowanie (tajność):**  
   - Alicja szyfruje wiadomość m kluczem publicznym Boba:  
     ```
     c = Enc(Kₑᴮ, m)
     ```  
   - Bob odszyfrowuje:  
     ```
     m = Dec(K_dᴮ, c)
     ```  
   - **Tylko Bob ma K_dᴮ ⇒ tylko on może odczytać m**.
2. **Podpis cyfrowy (autentyczność, nieodrzeczalność):**  
   - Role kluczy zamienione: prywatny Alicji (K_dᴬ) i publiczny Alicji (Kₑᴬ).  
   - Alicja “szyfruje” (podpisuje) m:  
     ```
     s = S(K_dᴬ, m)
     ```  
   - Każdy weryfikuje podpis:  
     ```
     V(Kₑᴬ, m, s) ⇒ true/false
     ```  
   - Dowodzi, że tylko **Alicja (znająca K_dᴬ) mogła stworzyć s**.

---

## 4. Atak _man-in-the-middle_  
- **Scenariusz:** Mariola podszywa się naprzemiennie pod Alicję i Boba:  
    - Mariola jako Alicja → Bolek: podaje klucz publiczny
    - Bolek → Mariola jako Alicja: szyfruje wiadomość dla Alicji
    - Mariola jako Bolek → Alicja: podaje klucz publiczny
    - Alicja → Mariola jako Bolek: szyfruje wiadomość dla Bolka
    - Alicja i Bolek myślą, że rozmawiają ze sobą
    - ale cała korespondencja przechodzi przez Mariolę  
- **Konsekwencja:** Alicja i Bob myślą, że rozmawiają ze sobą, ale wszystkie wiadomości przechodzą przez Mariolę.  
- **Obrona:**  
  - **Uwierzytelnianie** kluczy publicznych – upewnienie się, że klucz rzeczywiście należy do deklarowanej osoby.  
  - System certyfikatów, wzmocnione protokoły wymiany.

---

## 5. Kryptografia asymetryczna, cechy
- W kryptografii symetrycznej **uwierzytelnianie jest łatwe**
    - Bolek wie, że skoro wiadomość jest zaszyfrowana
    wspólnym kluczem Kab , to autorem musi być Alicja
    - ale nie może tego udowodnić przed sądem, skoro on też
    może przygotować taką wiadomość
- W kryptografii asymetrycznej **tylko Alicja może zaszyfrować wiadomość swoim kluczem prywatnym**
    - nie tylko Bolek może to sprawdzić, każdy może
    - w zasadzie sprawdzić można jedynie, że Ke oraz Kd
    stanowią parę
    - pozostaje problem związku Alicji z tą parą kluczy
- Mariola ogłasza, że klucz publiczny należy do Alicji i podpisuje dokument
    - Bolek weryfikuje, że podpis został złożony przez pasujący klucz prywatny
    - to nie to samo, co pewność, że podpis złożyła Alicja
- **Zalety**:
    - nie ma konieczności wcześniejszej wymiany tajnego klucza
    - klucz prywatny nie jest z nikim wymieniany
    - jest tylko jeden taki klucz
- **Wady**:
    - zdecydowanie mniejsza wydajność
        - więcej się szyfruje i uwierzytelnia (serwery)
        - zasoby są mniejsze (karta kryptograficzna) niż w kryptografii symetrycznej
    - problem uwierzytelnienia klucza publicznego
        - Mariola ogłasza, że klucz publiczny należy do Alicji
        - a Bolek sądzi, że komunikuje się z Alicją oraz, że ona jest autorką podpisanych dokumentów

---

## 6. Teoretyczne własności kryptografii asymetrycznej  
1. **Odpowiednik odporności na atak z wybranym tekstem jawnym:**  
   - Szyfr asymetryczny musi być _niedeterministyczny_, bo klucz publiczny jest jawny.  
2. **Wielokrotne szyfrowanie:**  
   - Odporność na atak z wielokrotnym szyfrowaniem jest równoważna (bez formalnego dowodu).  
3. **Brak idealnego szyfru:**  
   - Dla każdego klucza publicznego istnieje algorytm sprawdzający wszystkie możliwe klucze prywatne; bezpieczeństwo opiera się na złożoności obliczeniowej.

---

## 7. Szyfr hybrydowy  
Łączy zalety obu podejść:  
1. **Szyfrowanie:**  
   - Generujemy jednorazowy klucz sesyjny K (symetryczny).  
   - Szyfrujemy K kluczem publicznym odbiorcy:  
     ```
     C₁ = Enc_asym(Kₑ, K)
     ```  
   - Szyfrujemy wiadomość m kluczem sesyjnym:  
     ```
     C₂ = Enc_sym(K, m)
     ```  
   - Końcowy szyfrogram: para (C₁, C₂).  
2. **Odszyfrowanie:**  
   1. K = Dec_asym(K_d, C₁)  
   2. m = Dec_sym(K, C₂)  

### Zalety szyfru hybrydowego  
- Wydajność porównywalna do kryptografii symetrycznej (z minimalnym narzutem na klucz sesyjny).  
- Nie wymaga wymiany klucza prywatnego.  
- Jeśli obie części są odporne na odpowiednie ataki, cały system również.

---

## 8. Podpis cyfrowy w praktyce  
- **Problem wydajności:** podpisywanie długich wiadomości kluczem asymetrycznym jest kosztowne.  
- **Rozwiązanie:**  
  1. Obliczamy skrót wiadomości:  
     ```
     h = H(m)
     ```  
  2. Podpisujemy skrót kluczem prywatnym:  
     ```
     s = S(K_d, h)
     ```  
  3. Para podpisana: ⟨m, s⟩.  
  4. Weryfikacja:  
     ```
     V(Kₑ, h, s)  i  (h == H(m))
     ```  
- **Wniosek:** w praktyce weryfikuje się podpis skrótu, co jest efektywne i bezpieczne.

---

## 9. Ataki na funkcje skrótu i obrona  
### 8.1. Atak kolizyjny (Alice-Bob)  
1. Alicja ma dwie wersje m₁ i m₂, obie mogą zostać podpisane.  
2. Oblicza skróty h(m₁), h(m₂) i szuka kolizji: h(m₁) = h(m₂).  
3. Bolek podpisuje jedną (np. m₂): s = S(K_d, h(m₂)).  
4. Alicja twierdzi, że Bolek podpisał m₁, bo h(m₁) = h(m₂).  

**Wniosek:** funkcja skrótu używana do podpisu cyfrowego musi być silnie odporna na kolizje – _collision-resistant_.

### 8.2. Obrona przed atakami na funkcje skrótu  
- **Długość wyjścia:** co najmniej 2× długiej klucza symetrycznego (min. 160 lub 224 bity).  
- **Skróty z uwzględnieniem długości:** H(m ∥ len(m)) – utrudnia ataki drugiego preobrazu.  
- **Przebudowa wiadomości do podpisu:** włączenie elementów losowych lub unikalnego ID, by zmodyfikowana wiadomość była od razu odrzucana.

---

> **Podsumowanie:**  
> - **Kryptografia symetryczna**: szybka, ale wymaga bezpiecznej wymiany klucza.  
> - **Kryptografia asymetryczna**: eliminuje problem wymiany klucza prywatnego, ale jest wolniejsza i wymaga uwierzytelniania kluczy publicznych.  
> - **Szyfr hybrydowy** łączy obie metody, używając asymetryki do bezpiecznej dystrybucji klucza sesyjnego i symetryki do szyfrowania danych.  
> - **Podpis cyfrowy** + **funkcje skrótu** to standard dla autentyczności i integralności w praktycznych systemach kryptograficznych.  