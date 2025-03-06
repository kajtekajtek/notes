# Preprocessing danych
## I Usuwanie blednych danych
1. **Bledy w strukturze bazy** (nierowne wymiary wiersza/kolumny, brak separatorow itp)
2. **Bledy w formacie kolumn** (czy maja dane tego samego typu?)
3. **Bledy w danych** 
	[[#Metody identyfikacji obserwacji odstajacych|Dane spoza zakresu]]
## II Usuwanie brakujacych danych
*puste komorki, biale znaki, ?, -, --, b/d, n/a, NA, NaN, ...*
- [[#Sposoby na pozbycie sie brakujacych danych]]

## III Optymalizowanie struktury datasetu
- **Imbalanced data**
	Przy dysproporcji 1:10, 1:100, 1:1000 warto [[#Metody balansowania danych|zbalansowac dane]]
- **Rozmiar**
	Usuwanie kolumn, kompresja (algorytm PCA)

## IV Normalizacja danych
- [[#Sposoby normalizacji danych]]

# Metody identyfikacji obserwacji odstajacych
 - **rozstep miedzykwantylowy**
$$IQR = Q_3 - Q_1$$
$$DobryPrzedzial = [Q_1 - 1.5\cdot IQR, Q_3 + 1.5\cdot IQR]$$
- **z-score** (standardowy wynik)
$$z=\frac{\mu}{\sigma}$$

# Sposoby na pozbycie sie brakujacych danych
- **Deletion**
- **Imputation**: wstaw *srednia/mediane/dominante/k najblizszych sasiadow*

# Metody balansowania danych
- usuwanie nadmiernych probek (**under-sampling**)
- dodawanie kopii probek (**over-sampling**)
- generowanie **syntetycznych probek**

# Sposoby normalizacji danych
- Skalowanie / norm. min-max (**scale, mix-max scaling**)	$$y=\frac{x-min}{max-min}$$
- Standaryzacja, norm. z-score
	Dane sa oddalone przecietnie od 0 o 1, inaczej: przyjmuja rozklad normalny
$$y=\frac{x-\mu}{\sigma}$$