# Preprocessing danych
## I Usuwanie blednych danych
1. **Bledy w strukturze bazy** (nierowne wymiary wiersza/kolumny, brak separatorow itp)
2. **Bledy w formacie kolumn** (czy maja dane tego samego typu?)
3. **Bledy w danych** 
    - [Dane spoza zakresu](#Metody%20identyfikacji%20obserwacji%20odstajacych)
## II Usuwanie brakujacych danych
*puste komorki, biale znaki, ?, -, --, b/d, n/a, NA, NaN, ...*
- [Sposoby na pozbycie sie brakujacych danych](#Sposoby%20na%20pozbycie%20sie%20brakujacych%20danych)

## III Optymalizowanie struktury datasetu
- **Imbalanced data**
	Przy dysproporcji 1:10, 1:100, 1:1000 warto [zbalansowac dane](#Metody%20balansowania%20danych)
- **Rozmiar**
	Usuwanie kolumn, [PCA (Principal Component Analysis)](#PCA%20(Principal%20Component%20Analysis))

## IV Normalizacja danych
- [Sposoby normalizacji danych](#Sposoby%20normalizacji%20danych)

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

# PCA (Principal Component Analysis)
> Algorytm kondensuje informacje z bazy danych w nowo utworzonych zmiennych/kolumnach. Najpierw „upycha” jak najwięcej informacji w pierwszej nowej kolumnie. To co się nie udało, upycha do drugiej, resztki do trzeciej i tak dalej. W konsekwencji, pierwsze kolumny zawierają najwięcej informacji, a ostatnie najmniej. Ostatnie kolumny można usunąć z bazy danych bez dużej straty informacji.