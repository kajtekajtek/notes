# Uwierzytelnianie

## Metody uwierzytelniania  
- **Co użytkownik wie:** hasło, PIN, protokoły wiedzy zerowej.  
- **Co użytkownik ma:** token, karta, klucz prywatny.  
- **Cechy indywidualne:** odcisk palca, siatkówka oka, kształt twarzy.  
- **Zachowania:** podpis odręczny, głos, wzorzec pisania/chodzenia.  
- **Problemy:**  
  - wiedza może być podglądnięta lub wykradziona,  
  - przedmiot traci się lub uszkadza,  
  - cechy biometryczne są niezmienne.

## Uwierzytelnianie za pomocą haseł  
- hasło przesyłane wprost – tylko w lokalnych systemach  
- serwer przechowuje skróty h(p‖s), gdzie s = salt (losowe ziarno)  
- przy logowaniu porównuje się h(wpisane_hasło‖s)  
- łączenie z challenge–response → hasło + nonce (jednorazowy numer)

## Ataki na hasła  
- **Kradzież**: podglądanie, keylogger, wirus, kopie papierowe.  
- **Phishing**: podszywanie się pod serwis.  
- **Zgadywanie**: brutalne, słownikowe, rainbow tables (tęczowe tablice skrótów).  
- **Hasła domyślne** i stare „wycieki” – większość użytkowników ich nie zmienia.

## Obrona przed atakami na hasła  
- **Hasła spoza słownika**: testowe łamanie przy generowaniu hasła.  
- **Długie hasła** (>12 znaków) z różnymi klasami znaków.  
- **Solenie (salting):**  
  - unikalne ziarno s dla każdego hasła → h(p‖s)  
  - eliminuje rainbow tables, ale nie znosi konieczności dłubania w testach.  
- **Iteracyjne solenie:**  
  - przechowujemy h(h(...h(p‖s)‖s')…), większy koszt odtworzenia (Proof-of-Work).  
- **Wymiana haseł:**  
  - okresowo lub jednorazowo (OTP, SMS).  
  - single sign-on zmniejsza liczbę haseł.

## Klucze kryptograficzne  
- **Moc szyfrowania** zależy od długości klucza → przestrzeń ~2ⁿ.  
- **Symetryczne**: atak brutalny O(2ⁿ).  
- **Asymetryczne**:  
  - RSA/DH ≈ exp(n¹ᐟ³),  
  - krzywe eliptyczne znacznie trudniejsze do złamania przy krótszych kluczach.  
- **Przykładowe pary długości:**  
  | klucz symetryczny | RSA/DH (odpowiednik) |  
  |:-----------------:|:--------------------:|  
  |  80 bitów         |  768 bitów           |  
  | 128 bitów         | 2304 bitów           |

## Jakość haseł i kluczy  
- **Hasło ≠ 8 bitów:**  
  - ASCII ≈ 95 znaków → ~6,6 bitów na znak.  
  - Litery+cyfry+symbole → ≈6–7 bitów/znak.  
- **Przeciwdziałanie:** dłuższe hasła, passphrase, PBKDF2/scrypt/Argon2, solenie.  
- **Klucze losowe:** generowane z kryptograficznego PRNG, nie z entropii użytkownika.

## Problemy z uzgodnieniem i dystrybucją kluczy  
- **Symetryczne:** wymaga wstępnej dystrybucji klucza w bezpiecznym kanale lub za pośrednictwem zaufanego centrum.  
- **Asymetryczne:**  
  - dystrybucja publicznego klucza przez PKI lub web-of-trust,  
  - uwierzytelnienie klucza (man-in-the-middle),  
  - niższa wydajność, wymaga uwierzytelniania.

## Przekazywanie kluczy  
- **Wstępna dystrybucja:** długoterminowe klucze (asymetryczne) generowane i przekazywane wcześniej.  
- **Sesyjne klucze symetryczne:** generowane ad hoc, zabezpieczone kanałem ustanowionym kluczem asymetrycznym.  
- **Perfect forward secrecy:** losowe klucze sesyjne niemożliwe do odtworzenia po złamaniu klucza długo-terminowego.

## Aktualizacja kluczy  
- generowanie nowych kluczy sesyjnych – ochrona przed kryptanalizą z dużą ilością danych  
- funkcja aktualizująca (jednokierunkowa) chroni przyszłe klucze nawet po kompromitacji przeszłych

## Przechowywanie kluczy  
- **Sprzętowe HSM / karty kryptograficzne**  
- **Zaszyfrowane pliki** (hasło do odszyfrowania)  
- **Podział klucza** (secret sharing):  
  - Shamir’s t-of-n: dowolnych t uczestników może odtworzyć klucz, mniej – nie.  
- **Schemat progowy Blooma:** zaufany generator, uczestnicy otrzymują publiczne rᵢ i prywatne aᵢ, bᵢ; wspólny klucz = a + b·r.