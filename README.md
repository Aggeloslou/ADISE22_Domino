# ADISE22_Domino

Η εργασία αυτή γίνεται στα πλαίσια του μαθήματος Ανάπτυξη Διαδικτυακών Συστημάτων & Εφαρμογών που διδάσκεται στο χειμερινό εξάμηνο για το έτος 2022 στο Τμήμα Πληροφορικής και Ηλεκτρονικής Διεθνούς Πανεπιστήμιου Ελλάδος (ΔΙΠΑΕ). Η Εργασία αυτή υλοποιείται στην αρχιτεκτονική WebAPI σε php/mysql/ajax/ (jquery).

This project is being carried out as part of the course "Web Systems & Applications Development," which is being taught during the winter semester of 2022 in the Department of Informatics and Electronics at the International University of Greece (DIPAE). This project is implemented using the WebAPI architecture in PHP/MySQL/AJAX (jQuery).

## Σκοπός του παιχνιδιού - PURPOSE OF GAME

Σκοπός του παιχνιδιού είναι να τοποθετήσει πρώτος
ο παίκτης όλα τα πλακίδια του στο τραπέζι. Δηλαδή ο παίχτης που
δεν θα έχει άλλα πλακίδια στο χέρι του είναι και ο Νικητής. Τοποθετώντας τα σωστά πλακίδια
στους πίνακες.

The objective of the game is for a player to be the first
to place all of their tiles on the table. In other words, the player who has no tiles left in their hand is the winner. By placing the correct tiles on the boards.

ΚΑΝΟΝΕΣ ΠΑΙΧΝΙΔΙΟΎ - RULES OF  GAME
ΑΝ είναι κάτω στο board πχ. 2-4, 4-6 ο παίχτης χ θα πρέπει να παίξει ένα πλακίδιο οπού αποτελείτε
με 2 η 6 αλλιώς μπορεί και να τραβήξει αλλιώς θα χάσει την σειρά του
Ο παίχτης που μένει χωρίς πλακίδια κερδίζει.

If the board shows, for example, 2-4 or 4-6, player X must play a tile consisting of a 2 or a 6; otherwise, they may draw a tile, or they will lose their turn. The player who runs out of tiles first wins.


## Το project - THE PROJECT 
Το project αποτελείτε από την βάση που περιέχει τους πίνακες
board, board_empty, gamestatus, players, sharetile, tile
επισεις υπάρχει ενασ πίνακας clonetile για την βοήθεια
να μοιράσουμε τα tiles έτσι ώστε να μην έχουμε διπλό έγραφες και επισεις η βάση ολοκληρώνεται
με τα procedure check_aboard,check_play,cherck_result,cleanboard,draw_tile,play_tile,
tile_shuffle,update_sharetile,update_turn,first_move.

Έπειτα είναι υλοποιημένο σε php για το API κώδικα με με ($. ajax) javascript κώδικα για την μεριά του client Και τα κατάλληλα css
για τα html αρχεία και to bootstrap

Ενώ από την μεριά του server είναι υλοποιημένο σε php χρησιμοποιώντας σε php/mysql/ (jquery).
όπου έχουμε τα 4 αρχεία board. php, game. php, players. php για την εφαρμογή και για τη σύνδεση της βάσης
το dbconnnection. php


The project consists of a database containing the following tables:
board, board_empty, gamestatus, players, sharetile, tile
There is also a clonetile table to help
distribute the tiles so that there are no duplicates, and the database is completed with the procedures check_aboard, check_play, check_result, cleanboard, draw_tile, play_tile,
tile_shuffle, update_sharetile, update_turn, and first_move.

It is then implemented in PHP for the API, with JavaScript code using $.ajax for the client side, and the appropriate CSS
for the HTML files and Bootstrap

On the server side, it is implemented in PHP using PHP/MySQL/jQuery. We have the four files board.php, game.php, and players.php for the application, and dbconnection.php for the database connection.


## API Reference

---

### 👤 PLAYERS

#### Get all players

```http
GET /API/domino.php/players
```

```json
[
  { "name": "aggelos", "id": 1 },
  { "name": "aggelos2", "id": 2 }
]
```

🇬🇷 Η μέθοδος αυτή επιστρέφει τα ονόματα και τα id από τον πίνακα `players`, ώστε να ελέγξουμε αν υπάρχουν αρκετοί παίκτες για να ξεκινήσει το παιχνίδι.

🇬🇧 This method returns the names and IDs from the `players` table, so we can determine whether there are enough players for the game to start.

---

#### Get player by ID

```http
GET /API/domino.php/players/1
```

```json
{
  "name": "aggelos"
}
```

🇬🇷 Επιστρέφει τον παίκτη με ID = 1.  
🇬🇧 Returns the player with ID = 1.

---

#### Create player

```http
PUT /API/domino.php/players
```

```json
{
  "name": "aggelos"
}
```

🇬🇷 Καταχωρεί έναν νέο παίκτη στη βάση. Μόνο το όνομα απαιτείται. Τα υπόλοιπα πεδία δημιουργούνται αυτόματα.  
Το `result` γίνεται `"win"` μόνο όταν ο παίκτης δεν έχει άλλα domino.

🇬🇧 Creates a new player. Only the name is required. Other fields are automatically generated.  
`result` becomes `"win"` only when the player has no tiles left.

---

### 📊 PLAYERS TABLE

| Parameter | Type | Description |
|----------|------|------------|
| id | int | NOT NULL AUTO_INCREMENT |
| name | varchar | Player name |
| token | varchar | MD5 token |
| last_action | timestamp | auto update |
| result | varchar | DEFAULT NULL ("win") |

---

### 🎲 BOARD

#### Get board

```http
GET /API/domino.php/board
```

```json
[
  {
    "bid": "1",
    "btile": null,
    "last_change": "2023-01-08 01:03:09"
  },
  {
    "bid": "2",
    "btile": null,
    "last_change": "2023-01-08 01:03:09"
  }
]
```

🇬🇷 Επιστρέφει την κατάσταση του board.  
🇬🇧 Returns the current board state.

---

#### Initialize board

```http
POST /API/domino.php/board
```

🇬🇷 Ο πίνακας board αρχικά είναι άδειος.  
🇬🇧 The board table is initially empty.

---

### 📊 BOARD TABLE

| Parameter | Type | Description |
|----------|------|------------|
| bid | enum('1','2') | Primary key |
| btile | varchar | Tile placed |
| firstvalue | int | Value |
| secondvalue | int | Value |
| last_change | timestamp | Last update |

---

### 🧩 TILES

#### Get all tiles

```http
GET /API/domino.php/tiles
```

```json
[
  {
    "id": 0,
    "tile_name": "0-6",
    "player_name": "aggelos"
  },
  {
    "id": 1,
    "tile_name": "3-4",
    "player_name": "aggelos2"
  }
]
```

🇬🇷 Επιστρέφει όλα τα tiles μοιρασμένα στους παίκτες.  
🇬🇧 Returns all distributed tiles.

---

#### Get tiles by player

```http
GET /API/domino.php/tiles/aggelos
```

```json
[
  {
    "id": 0,
    "tile_name": "0-6",
    "player_name": "aggelos"
  },
  {
    "id": 12,
    "tile_name": "3-5",
    "player_name": "aggelos"
  }
]
```

🇬🇷 Επιστρέφει τα tiles του παίκτη aggelos.  
🇬🇧 Returns tiles of player aggelos.

---

#### Distribute tiles

```http
PUT /API/domino.php/tiles
```

🇬🇷 Μοιράζει 7 tiles σε κάθε παίκτη.  
🇬🇧 Distributes 7 tiles to each player.

---

### 📊 TABLES

#### tile

| Parameter | Type |
|----------|------|
| tilename | varchar |
| firstvalue | int |
| secondvalue | int |

#### sharetile

| Parameter | Type |
|----------|------|
| id | int |
| tile_name | varchar |
| player_name | varchar |

---

### 🎮 GAME STATUS

#### Get status

```http
GET /API/domino.php/status
```

```json
{
  "id": 1,
  "status": "started",
  "p_turn": "1",
  "last_change": "2023-01-08 21:08:18"
}
```

🇬🇷 Επιστρέφει την κατάσταση του παιχνιδιού.  
🇬🇧 Returns the current game status.

---

### 📊 GAMESTATUS TABLE

| Parameter | Type | Description |
|----------|------|------------|
| id | int | Primary key |
| status | varchar | initialized, started, ended, aborted |
| p_turn | int | Player turn |
| last_change | timestamp | Last update |

---

### ▶️ PLAY

#### Get play state

```http
GET /API/domino.php/play
```

🇬🇷 Εμφανίζει την κατάσταση του board.  
🇬🇧 Returns the board state.

---

#### Play tile

```http
PUT /API/domino.php/play
```

🇬🇷 Καλεί τη συνάρτηση:
```
play_tile(tile_name, player_name)
```
και ενημερώνει:
- board
- σειρά παικτών

🇬🇧 Calls function:
```
play_tile(tile_name, player_name)
```
and updates:
- board
- turn order

---

### ❌ ABORT

#### Abort game

```http
GET /API/domino.php/abort
```

🇬🇷 Τερματίζει το παιχνίδι καλώντας τη συνάρτηση `check_abort`.  
🇬🇧 Ends the game by calling `check_abort`.

---

### 🎯 DRAW TILE

#### Draw tile

```http
PUT /API/domino.php/draw
```

🇬🇷 Επιτρέπει σε παίκτη να τραβήξει ένα tile (προστίθεται νέο tile στο sharetile).  
🇬🇧 Allows a player to draw a new tile (adds a tile in sharetile).

---



## Authors

    ΛΟΥΣΙ ΑΝΤΖΕΛΟ 144347
    ADISE22_DOMINO

Free for educational use
