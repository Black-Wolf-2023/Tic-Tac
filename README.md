
## Tic-Tac Game ( Composition Api Vue 3  and mitt Event Controller)


### Game elements

* 2 Players (X and O)
* The Board Grid (3 rows × 3 columns = 9 cells)
* Scoreboard (The number of wins for each player)
* Number of match being played
* Player turn
* Restarting the game

## Workflow

* [x] Init the project with (vue-cli)
* [x] Add google fonts to (index.html): [Dosis & Permanent Marker]
* [x] Edit App component (change styles)
* [x] Create the grid component & styling it
* [x] Create the cell component & styling it
* [x] Specify Data Properties (APP)
  * Number of matches
  * Number of wins for each player
* [x] Specify Data Properties (GRID)
  * Active Player (X or O)
  * Game Status (turn - win - draw)
  * Status Message ( O's turn / X's turn )
  * Status Color
    * statusTurn (default) is yellow for a turn
    * statusWin is green for a win
    * statusDraw is gray for a draw
  * Number of moves played by both players  (max=9)
  * Winning Conditions
  * Mark placement for each cell
* [x] Specify Data Properties (CELL)
* [x] Event Bus
* [x] Start game (Listening For shots)
  * listen to 'shot' event
  * fill the respective cell number with the mark in the cells object
  * increment the number of moves
  * change the game status and change the active player
  * Check game status
* [x] Displaying the Status
* [x] Checking for a Win
* [x] Scoreboard
* [x] Restarting the Game
* [x] Number of Matches


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
