
# Dokumentacja API Serwisu Gry w Kółko i Krzyżyk

## Podstawowy URL
- **URL:** `{BASE_URL}` (Zastąp `{BASE_URL}` rzeczywistym podstawowym adresem URL usługi)

## Punkty końcowe

### 1. Utwórz Nową Grę
- **Metoda:** `POST`
- **Endpoint:** `/game`
- **Opis:** Tworzy nową instancję gry.
- **Body żądania:** Brak
- **Odpowiedzi:**
  - **201 Utworzono**
    - **Body:** 
      ```json
      {
        "message": "New game created",
        "game_id": [integer]
      }
      ```
- **Przykładowe żądanie:**
  ```bash
  curl -X POST {BASE_URL}/game
  ```

### 2. Wykonaj Ruch
- **Metoda:** `POST`
- **Endpoint:** `/game/{game_id}/move`
- **Opis:** Wykonuje ruch w istniejącej grze.
- **Parametry URL:**
  - `game_id` (wymagane): ID gry, w której wykonuje się ruch.
- **Body żądania:** (wymagane)
  - **Typ zawartości:** `application/json`
  - **Pola:**
    - `cellIndex`: Indeks komórki, w której wykonuje się ruch (0-8).
- **Odpowiedzi:**
  - **200 OK**
    - **Body:** 
      ```json
      {
        "message": "Move made",
        "game_id": [integer],
        "moves": "string"
      }
      ```
  - **400 Złe Żądanie**
    - **Body:** 
      ```json
      {
        "message": "Cell is already occupied" | "Move data is required"
      }
      ```
  - **404 Nie Znaleziono**
    - **Body:** 
      ```json
      {
        "error": "Game not found"
      }
      ```
- **Przykładowe żądanie:**
  ```bash
  curl -X POST -H "Content-Type: application/json" -d '{"cellIndex": 4}' {BASE_URL}/game/1/move
  ```

### 3. Pobierz Szczegóły Gry
- **Metoda:** `GET`
- **Endpoint:** `/game/{game_id}`
- **Opis:** Pobiera aktualny stan gry.
- **Parametry URL:**
  - `game_id` (wymagane): ID gry do pobrania.
- **Odpowiedzi:**
  - **200 OK**
    - **Body:** 
      ```json
      {
        "game_id": [integer],
        "moves": "string"
      }
      ```
  - **404 Nie Znaleziono**
    - **Body:** 
      ```json
      {
        "error": "Game not found"
      }
      ```
- **Przykładowe żądanie:**
  ```bash
  curl {BASE_URL}/game/1
  ```

## Obsługa Błędów
Błędy są zwracane jako standardowe kody statusu HTTP wraz z odpowiedzią JSON zawierającą wiadomość o błędzie.

## Uwagi
- String `moves` w odpowiedzi reprezentuje sekwencję wykonanych dotąd ruchów w grze. Każdy ruch reprezentowany jest przez dwa znaki: pierwszy to indeks komórki (0-8), a drugi wskazuje gracza ('X' lub 'O').

Zastąp `{BASE_URL}` rzeczywistym podstawowym adresem URL, pod którym hostowana jest usługa, podczas wykonywania żądań.
