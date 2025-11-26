# Entrance_Identification_Solution

## 1. Streszczenie projektu

Celem jest webowy system kontroli wejść dla dużej fabryki, który łączy: skan ważnej przepustki (QR code) oraz automatyczną identyfikację osoby przez twarz w momencie wejścia. System ma rejestrować wszystkie próby wejścia (udane i nieudane), zapisywać metadane identyfikacyjne, prowadzić rejestr uprawnień pracowników, oraz generować raporty o nadużyciach i efektywności.

### Kluczowe wymagania:

* Autoryzacja na podstawie ważnej przepustki QR + zgodność wizerunku twarzy z profilem pracownika

* Rejestracja wszystkich prób wejścia z dokładnym logiem (czas, punkt, zdjęcie, wynik identyfikacji, operator/automat)

* Panel administracyjny do zarządzania uprawnieniami i listą osób uprawnionych

* Raporty: przypadki współdzielenia kart, odrzucenia wejść, mismatche twarzy, statystyki czasu pracy

* Audyt i eksport (CSV/PDF)

* Prywatność i zgodność z RODO (retencja obrazów, dostęp, szyfrowanie)

## 2. Dokumentacja techniczna - potencjalna

* Frontend: HTML + JS (kamera, skan QR, panel admina)
* Backend: FastAPI (REST API)
* Face Recognition: Azure Face API (domyślnie) / opcjonalnie lokalny model
* Baza danych: SQLite (dev) / PostgreSQL (prod)
* Storage: lokalny katalog /data/images/

## 3. Wymagania funkcjonalne (high-level)

Przy próbie wejścia: system przyjmuje zdjęcie twarzy + odczyt QR. Weryfikuje ważność przepustki i porównuje twarz z rekordem pracownika powiązanym z tą przepustką.
Jeżeli twarz pasuje i przepustka ważna -> wejście zatwierdzone i zapis. Jeżeli pasuje przepustka ważna ale twarz nie pasuje -> odnotować jako "podejrzenie nadużycia" i zablokować/wyjątkowo wymusić interwencję.
Wszystkie zdarzenia logowane z: timestamp, punkt wejścia, id przepustki, id pracownika (jeśli dopasowano), score dopasowania twarzy, zdjęcie (thumbnail) i pełne zdjęcie (retencja zależna od polityki), operator (jeżeli interwencja).
Panel admina: CRUD pracowników, przepustek, uprawnień, list punktów wejścia, przegląd logów, generowanie raportów.
Raporty: listy nadużyć (kiedy przepustka użyta przez inną osobę), statystyki (odrzuconych wejść / procent dopasowań), eksport CSV/PDF.


## 4. Instalacja i uruchomienie
1. Sklonuj repozytorium:
```
git clone <repo_url>
cd entrance_Identification_Solution
```
2. Utwórz wirtualne środowisko i aktywuj je:
```
python -m venv venv
source venv/bin/activate      # Linux/macOS
venv\Scripts\activate         # Windows
```
3. Zainstaluj wszystkie zależności:
```
pip install --upgrade pip
pip install -r requirements.txt
```
4. Skopiuj plik środowiskowy i ustaw swoje zmienne:

5. Uruchom aplikację:
```
bash run.sh
```

6. Wejdź w przeglądarce:
   * Frontend:
   * Panel admin: 