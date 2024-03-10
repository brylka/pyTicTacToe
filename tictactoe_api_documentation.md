
# Tic Tac Toe Game Service API Documentation

## Base URL
- **URL:** `{BASE_URL}` (Replace `{BASE_URL}` with the actual base URL of the service)

## Endpoints

### 1. Create a New Game
- **Method:** `POST`
- **Endpoint:** `/game`
- **Description:** Creates a new game instance.
- **Request Body:** None
- **Responses:**
  - **201 Created**
    - **Body:** 
      ```json
      {
        "message": "New game created",
        "game_id": [integer]
      }
      ```
- **Example Request:**
  ```bash
  curl -X POST {BASE_URL}/game
  ```

### 2. Make a Move
- **Method:** `POST`
- **Endpoint:** `/game/{game_id}/move`
- **Description:** Makes a move in an existing game.
- **URL Parameters:**
  - `game_id` (required): The ID of the game where the move is being made.
- **Request Body:** (required)
  - **Content-Type:** `application/json`
  - **Fields:**
    - `cellIndex`: The index of the cell where the move is made (0-8).
- **Responses:**
  - **200 OK**
    - **Body:** 
      ```json
      {
        "message": "Move made",
        "game_id": [integer],
        "moves": "string"
      }
      ```
  - **400 Bad Request**
    - **Body:** 
      ```json
      {
        "message": "Cell is already occupied" | "Move data is required"
      }
      ```
  - **404 Not Found**
    - **Body:** 
      ```json
      {
        "error": "Game not found"
      }
      ```
- **Example Request:**
  ```bash
  curl -X POST -H "Content-Type: application/json" -d '{"cellIndex": 4}' {BASE_URL}/game/1/move
  ```

### 3. Get Game Details
- **Method:** `GET`
- **Endpoint:** `/game/{game_id}`
- **Description:** Retrieves the current state of a game.
- **URL Parameters:**
  - `game_id` (required): The ID of the game to retrieve.
- **Responses:**
  - **200 OK**
    - **Body:** 
      ```json
      {
        "game_id": [integer],
        "moves": "string"
      }
      ```
  - **404 Not Found**
    - **Body:** 
      ```json
      {
        "error": "Game not found"
      }
      ```
- **Example Request:**
  ```bash
  curl {BASE_URL}/game/1
  ```

## Error Handling
Errors are returned as standard HTTP status codes, along with a JSON response containing a message about the error.

## Notes
- The `moves` string in the response represents the sequence of moves made in the game so far. Each move is represented by two characters: the first is the cell index (0-8), and the second indicates the player ('X' or 'O').

Replace `{BASE_URL}` with the actual base URL where the service is hosted when making requests.
