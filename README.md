A Java Battleship game with **dual UI implementations** (Console + Swing GUI) demonstrating **MVC architecture**, **interface-based design**,  and **testing practices**.

Architecture & Design:
- **MVC pattern**
- **Multiple UI implementations**
- **Interface-based design** for swappable components
- **Dependency Injection** and loose coupling
- **SOLID principles**

Test Coverage:
- **Model tests** - ship placement, hit detection, game state, win/loss conditions
- **Controller tests** - manual mocks + Mockito framework (practiced both approaches)

<div align="center">
  <table>
    <tr>
      <th colspan="2" style="text-align: center; padding: 10px; font-size: 18px;">Console Interface</th>
    </tr>
    <tr>
      <td style="text-align: center; padding: 10px;">
        <img src="imgs/bg1.jpg" alt="Game Start" height="300"/>
        <br><b>Game Start</b>
      </td>
      <td style="text-align: center; padding: 10px;">
        <img src="imgs/bg2.jpg" alt="Gameplay" height="300"/>
        <br><b>Gameplay</b>
      </td>
    </tr>
  </table>
</div>

<div align="center">
  <table>
    <th colspan="2" style="text-align: center; padding: 10px; font-size: 18px;">Swing GUI Interface</th>
    </tr>
    <tr>
      <td style="text-align: center; padding: 10px;">
        <img src="imgs/bg3.png" alt="Game Start" height="400"/>
        <br><b>Game Start</b>
      </td>
      <td style="text-align: center; padding: 10px;">
        <img src="imgs/bg4.png" alt="Gameplay" height="400"/>
        <br><b>Gameplay</b>
      </td>
    </tr>
  </table>
</div>

## Setup

**Requirements:** Java 17+   
**Required test libraries:** JUnit 5, Mockito 5.9.0, [byte-buddy](https://repo1.maven.org/maven2/net/bytebuddy/byte-buddy/), [byte-buddy-agent](https://repo1.maven.org/maven2/net/bytebuddy/byte-buddy-agent/), [mockito-core](https://repo1.maven.org/maven2/org/mockito/mockito-core/), [mockito-junit-jupiter](https://repo1.maven.org/maven2/org/mockito/mockito-junit-jupiter/), [objenesis](https://repo1.maven.org/maven2/org/objenesis/objenesis/)  

1. compile
```bash
javac -d bin src/main/java/battleship/**/*.java
```

2. run Console version
```bash
java -cp bin battleship.ConsoleApp
```

**OR** run Swing GUI version
```bash
java -cp bin battleship.SwingApp
```

## Usage

**Console Version:**
1. Launch → grid displays with hidden ships
2. Enter coordinates: `A5` (row A-J, column 0-9)
3. Get feedback: HIT/MISS, updated grid
4. Win: Sink all 5 ships | Lose: Use all 50 guesses

**Swing GUI Version:**
1. Launch → clickable grid interface
2. Click cells to guess
3. Visual feedback: color-coded hits/misses
4. Same win/loss conditions

**Valid Inputs:** `A5`, `a5`, `J9` (case-insensitive)  
**Invalid:** `K5` (out of bounds), `A10` (invalid column), duplicate guesses

**Ships:**
- Aircraft Carrier (5 cells)
- Battleship (4 cells)
- Submarine (3 cells)
- Destroyer (3 cells)
- Patrol Boat (2 cells)

## Architecture
```
src/main/java/battleship/
├── model/
│   ├── IBattleshipModel.java              # model contract
│   ├── BattleshipModel.java               # game logic
│   ├── ShipType.java                      # ship definitions
│   └── CellState.java                     # cell states (empty/hit/miss)
├── view/
│   ├── IBattleshipView.java               # view contract
│   ├── BattleshipConsoleView.java         # console UI
│   └── SwingBattleshipView.java           # GUI implementation
├── controller/
│   ├── IBattleshipController.java         # controller contract
│   ├── BattleshipConsoleController.java   # console controller
│   └── SwingBattleshipController.java     # GUI controller
├── ConsoleApp.java                        # console entry point
└── SwingApp.java                          # GUI entry point

src/test/java/battleship/
├── model/
│   ├── BattleshipModelPlacementTest.java          # ship placement logic
│   ├── BattleshipModelPlayerInteractionTest.java  # hit/miss mechanics
│   ├── BattleshipModelGameStateTest.java          # win/loss conditions
│   └── BattleshipModelIntegrationTest.java        # full game scenarios
└── controller/
    ├── BattleshipConsoleControllerTest.java           # manual mocks
    ├── BattleshipConsoleControllerMockitoTest.java    # Mockito mocks
    └── BattleshipConsoleControllerparseGuessTest.java # input parsing
```
