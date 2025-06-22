# Test Millera–Rabina  
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