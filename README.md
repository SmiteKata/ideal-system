# 🚀 Trello API Tests - CRUD Operations (Postman Collection)

Zbiór automatycznych testów weryfikujących pełny cykl życia zasobu **Tablica (Board)** w Trello API. Testy zostały zaprojektowane do uruchamiania w środowisku **Postman Collection Runner** lub z wiersza poleceń za pomocą **Newman**.

## 🎯 Scenariusz Testowy (Kroki E2E)

Testy następują po sobie w sekwencji, wykorzystując dane przekazane między żądaniami:

1.  **POST Create Board:** Tworzy nową tablicę i **zapisuje jej ID** do zmiennej kolekcji (`boardID`).
2.  **Weryfikacja POST:** Sprawdza poprawność kodu statusu (`200`), typu danych (`string`) oraz zgodność tytułu (`name`) z wartością wejściową.
3.  **PUT Update Board:** Edytuje tablicę o zapisanym `boardID`, zmieniając tytuł i opis.
4.  **Weryfikacja PUT:** Sprawdza poprawność kodu statusu (`200`) i zgodność nowego tytułu (`name`) oraz opisu (`desc`) z wartościami edytowanymi.
5.  **GET Board:** Pobiera dane edytowanej tablicy (test pozostawiony jako kontrola sukcesu).
6.  **DELETE Board:** Usuwa tablicę o zarejestrowanym `boardID`.
7.  **GET Verification:** **Kluczowa Weryfikacja:** Próbuje pobrać usunięty zasób, oczekując kodu błędu (`404 Not Found`), co potwierdza skuteczne usunięcie.

## 🔑 Wymagane Zmienne (Secrets Injection)

Zmienne autoryzacyjne (`Key`, `Token`) muszą być ustawione w aktywnym środowisku (lub wstrzyknięte przy użyciu Newmana), aby zachować bezpieczeństwo.

| Zmienna | Typ | Opis |
| :--- | :--- | :--- |
| `baseUrl-1.0` | Environment | Bazowy URL API Trello (np. `https://api.trello.com/1`) |
| **`Key`** | **Environment/Secret** | Klucz API do autoryzacji Trello. |
| **`Token`** | **Environment/Secret** | Token Access Token do autoryzacji Trello. |
| `boardID` | Collection | Przechowuje ID nowo utworzonej tablicy (ustawiane dynamicznie przez test POST). |

---

## ▶️ Instrukcja Uruchomienia w Postmanie

1.  **Import Kolekcji:** W Postmanie, zaimportuj plik `./collections/trello_crud.json`.
2.  **Import Środowiska:** Zaimportuj plik `./environments/trello_env_template.json`.
3.  **Uzupełnienie Sekretów:** W aktywnym środowisku, ręcznie uzupełnij pola **`Key`** i **`Token`** swoimi prywatnymi kluczami Trello.
4.  **Uruchomienie:** Użyj **Collection Runner** i wybierz zaimportowaną kolekcję oraz środowisko. Testy muszą być uruchamiane w kolejności.
