# Protokoły kryptograficzne

## Protokoły kryptograficzne  
- Wykonywane przez wielu uczestników, algorytm definiuje jednego wykonawcę.  
- Trzeba rozważyć ataki przez nieuprawnionych gości (man-in-the-middle).  
- **Wide‐mouth frog (protokół „żaby o szerokich ustach”):**  
  1. Alicja → Tadeusz: `id(A), E_A(T_A, id(B), K)` (T_A = znacznik czasu, K = klucz sesyjny).  
  2. Tadeusz → Bolek: `E_B(T_B, id(A), K)` (T_B = nowy znacznik czasu).  
  3. Bolek i Tadeusz weryfikują czas.  
- Wady: wysoki narzut dla pośrednika (Tadeusza) i uczestników (zsynchronizowany zegar).

## Atak powtórzeniowy (replay)  
- Mariola podsłuchuje i zapisuje komunikaty pośrednika do Boba.  
- Następnie wznawia je z opóźnieniem → Bolek myśli, że to nowe żądanie.  
- Obrona:  
  - Numerowanie wiadomości (sekwencje), uczestnicy odrzucają duplikaty.  
  - Krótkie okresy ważności znaczników czasu + synchronizacja zegarów.  
  - Wymaga losowych nonce: Alicja generuje liczby jednorazowe, Bob potwierdza każdą w odpowiedzi.

## Atak DoS (Denial of Service)  
- **Scenariusz:** Alicja żąda od Tadeusza przesłania komunikatu do Boba (np. żaba o szerokich ustach).  
- Tadeusz może być obciążony wieloma takimi żądaniami → przeciążenie.  
- **Przeciwdziałanie:**  
  - Protokół Needham–Schrödera z „biletami”:  
    1. A → T: `id(A), id(B), r_A` (losowe).  
    2. T → A: `E_A(r_A, id(B), K_AB, E_B(K_AB, id(A)))`.  
    3. A → B: `E_B(K_AB, id(A))`.  
  - Bilety ograniczają liczbę wiadomości wysyłanych przez pośrednika, przenosząc ciężar na uczestników.

## Kerberos  
- Opracowany w MIT, głównie symetrycznie, do uwierzytelniania w sieciach korporacyjnych.  
- **Założenia:**  
  - Jeden (lub kilka) centralnych serwerów uwierzytelniających (AS/TGS).  
  - Czas życia biletów ograniczony (znaczniki czasu).  
- **Kerberos v5 (upraszczony):**  
  1. A → AS: `id(A), id(B), r_A`.  
  2. AS → A: `E_{K_A}(K_{AB}, id(B), t_1, ticket_{TGS})`.  
  3. A → B: `ticket_{TGS}` + `E_{K_{AB}}(id(A), t_1)`.  
  4. B → A: `E_{K_{AB}}(t_1+1)`.  
- Uwierzytelnianie wieloetapowe z biletami i stemplami czasu.

## Własności Kerberosa  
- **Hierarchia:** TGS (Ticket‐Granting Server) wydaje bilety dostępu do serwisów.  
- **Synchronizacja czasów:** wymagana węzłowo, bilety ważne tylko w krótkim oknie czasowym.  
- **Asymetria roli:** użytkownik uwierzytelnia się wobec usługi, ale nie odwrotnie – protokół skoncentrowany na inicjatywie klienta.

## SSL/TLS  
- Standard dla bezpiecznego HTTP (HTTPS): Netscape 1994, IETF 1999.  
- **Przebieg handshake:**  
  1. A ↔ B: ustalenie wersji, algorytmów, wymiana nonce/certyfikatów.  
  2. A → B: `ClientKeyExchange` – klucz wstępny zaszyfrowany certyfikatem B.  
  3. W obu kierunkach: generacja kluczy sesyjnych z klucza wstępnego i nonce.  
- **Zabezpieczenia:**  
  - Stosowanie znaczników czasu i liczb jednorazowych uniemożliwia ataki typu replay.  
  - Uwierzytelnienie serwera (certyfikat), opcjonalne uwierzytelnienie klienta.  
  - Komunikacja szyfrowana i opatrzona MAC.