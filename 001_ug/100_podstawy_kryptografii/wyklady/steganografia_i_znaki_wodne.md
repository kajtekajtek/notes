# Steganografia i znaki wodne  

## Definicje  
- **Dzieło:** każdy artefakt cyfrowy lub analogowy – fotografia, film, utwór muzyczny, kod programu, dokument HTML, itp.  
- **Treść (content):** informacja, którą dzieło niesie.  
- **Nośnik:** sposób przechowywania lub transmisji dzieła – plik na dysku, CD/DVD, strumień TV/internet, wydruk, fotografia.

## Steganografia vs. znak wodny  

### Znakowanie (watermarking):  
  - Dodanie do dzieła informacji związanej z autorem, właścicielem lub warunkami użycia.  
  - Nieodczuwalne (lub minimalnie odczuwalne) przez odbiorcę, trudne do usunięcia.  

### Steganografia:  
  - Jednoczesne ukrycie dodatkowych danych (wiadomości) w dziele.  
  - Treść ukryta jest niezależna od oryginału, ma pozostać niezauważalna i tajna.

## Operacje  

### **Zanurzanie (embedding):**  
- **E**mbedding(**c**over work, **m**essage) → **c′**
- ukrycie wiadomości m w nośniku c, z opcjonalnym kluczem.  

### **Wykrywanie/wyodrębnianie (detecting/extracting):**  
- D(c′) → m
- odzyskanie m z c′; może wymagać klucza, a nawet oryginału.

## Zastosowania znaków wodnych  
- **Identyfikacja autora/właściciela:**  
– oznaczenie ograniczeń praw autorskich (©).  
– śledzenie źródeł nielegalnych kopii.  
- **Dowód autorstwa:**  
– umieszczony w dziele znak = zabezpieczony hasłem.  
– trudność fałszerstwa – czy można „udowodnić” nieistniejący znak?  
- **Monitorowanie dystrybucji:**  
– śledzenie przekazów reklamowych, dokumentów poufnych.  
- **Ochrona przed nadmiernym kopiowaniem:**  
– ograniczenie liczby dozwolonych kopii, wyśledzenie nadmiernego rozprzestrzeniania.  
- **Uwierzytelnianie dzieła:**  
– alternatywa lub uzupełnienie podpisu cyfrowego.  
- **Wielokrotne/ modyfikowalne znaki:**  
– różne warstwy informacji: numer kopii, dystrybutor, stan licencji.

## Własności systemów znaków wodnych  
- **Efektywność:** wysoka wykrywalność przy minimalnych zakłóceniach.  
- **Wierność:** odbiorca odbiera dzieło jako oryginalne.  
- **Nośność:** mały narzut (absolutny/ względny) do jakości nośnika.  
- **Wykrywanie ślepe vs. z oryginałem:**  
– publiczne (tylko c′) lub prywatne (c′ + c).  
- **Czułość / odporność:**  
– prawdopodobieństwo, że znak przetrwa określone modyfikacje (kompresja, filtracja).  
- **Specyficzność:**  
– niska szansa wykrycia znaku tam, gdzie go nie ma.

## Bezpieczeństwo steganografii  

### Ataki na systemy:
- **Tylko z dziełem ze znakiem:** próba usunięcia lub zaburzenia znaku.  
- **Z dostępem do oryginału:** porównanie c i c′ w celu wykrycia zmian.  
- **Z wybraną wiadomością:** atakujący prosi o ukrycie własnej treści, by analizować algorytm.  
- **Z adaptacyjnym dostępem:** żądanie wykrycia lub ekstrakcji dla wybranego c′.

### Ataki na pojedyncze dzieło:
- usunięcie (znika znak lub staje się nieczytelny)  
- falsyfikacja (wstawienie własnego znaku)  
- nieautoryzowane odczytanie (ekstrakcja m bez klucza)

## Przykłady implementacji – grafika  

### Metoda LSB (Least Significant Bit):
- Każdy piksel RGB ma 3 bajty; LSB każdego bajtu zmieniany na bit m.  
- Niewielka zmiana intensywności niewidoczna gołym okiem.  
- **Transformacje w dziedzinie częstotliwości:**  
    - Ukrywanie w przekształceniu dyskretnej kosinusoidy (DCT) lub falkowym.  
    - Odporność na kompresję JPEG/LZW.

## Przykłady implementacji – HTML  

### Ukryte spacje/tabulatory:
- Spacje na końcu wiersza lub w tagach – interpretowane równorzędnie przez przeglądarki.  
- Liczba spacji koduje bity.  
- **Fałszywe lub dodatkowe atrybuty w tagach:**  
    - Dowolna kolejność, wielkość liter i odstępy w tagach pozwalają na wstawianie znaków.

## Przykłady implementacji – tekst zwykły  

### **Spacje na końcu linii:**  
– niewidoczne, mogą kodować informację.  

### **Celowe literówki lub synonimy:**  
– słownik kontrolowany generuje maskę bitową.  

### **Generatory tekstu:**  
– gramatyki ukrywające wybory słów i strukturę zdania (np. spammimic.com).  

---