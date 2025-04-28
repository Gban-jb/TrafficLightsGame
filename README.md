📋 Traffic Light Game - Flutter Project
🚦 Overview
Traffic Light Game is a two-player interactive Flutter app where players take turns selecting cells on a 4x3 grid. Each cell represents a traffic light that changes states:

From empty → Green Circle → Yellow Triangle → Red Hexagon.

After reaching the Red Hexagon, the cell can no longer be changed.

The goal is for a player to form a sequence (row, column, or diagonal) of three identical shapes to win.

📂 Project Structure

File	Purpose
main.dart	Entry point of the Flutter application, initializes and runs the GameScreen.
game_screen.dart	Core gameplay logic, user interface, and custom shape painters for Circle, Triangle, and Hexagon.
🚀 How to Run
Make sure Flutter is installed (flutter doctor to verify).

Clone or download this project.

Open the project folder in VS Code (or any preferred IDE).

Run the following commands:

bash
Copy
Edit
flutter pub get
flutter run
🎮 Gameplay Rules
Turn-Based: Player 1 and Player 2 take turns tapping on a grid cell.

State Changes:

First tap: Empty → Green Circle

Second tap: Green Circle → Yellow Triangle

Third tap: Yellow Triangle → Red Hexagon

Restrictions:

A cell can be tapped only three times maximum (after that it’s locked).

Winning Condition:

A player wins if they align three of the same shapes (Green Circle, Yellow Triangle, or Red Hexagon) in:

A row (horizontal line),

A column (vertical line),

A diagonal (slanting line).

🛠️ Technical Concepts Explained (with Code Examples)
1. StatefulWidget
A widget that maintains dynamic state (data that can change during the app).

dart
Copy
Edit
class GameScreen extends StatefulWidget {
  const GameScreen({super.key});

  @override
  State<GameScreen> createState() => _GameScreenState();
}
Here, GameScreen needs to change its appearance when players take turns, so it’s a StatefulWidget.

2. List.generate
Creates lists dynamically, great for making grids.

dart
Copy
Edit
List<List<int>> grid = List.generate(4, (_) => List.filled(3, 0));
List<List<int>> changeCount = List.generate(4, (_) => List.filled(3, 0));
This creates:

A 4x3 matrix (4 rows, 3 columns) where each cell is initially 0.

3. CustomPainter
Used to draw custom shapes (circle, triangle, hexagon).

dart
Copy
Edit
class CirclePainter extends CustomPainter {
  final Color color;
  
  CirclePainter({required this.color});
  
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      ..color = color
      ..style = PaintingStyle.fill;
    
    canvas.drawCircle(
      Offset(size.width / 2, size.height / 2),
      size.width / 2,
      paint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}
Similarly, there are TrianglePainter and HexagonPainter.

4. GestureDetector
Captures tap events on each cell.

dart
Copy
Edit
GestureDetector(
  onTap: () => _handleTap(row, col),
  child: Container(
    width: 70,
    height: 70,
    child: Center(
      child: _getShape(grid[row][col]),
    ),
  ),
);
Each cell in the grid is wrapped in a GestureDetector to detect taps.

5. Scaffold
Provides a basic visual layout with an AppBar, body, and floating elements.

dart
Copy
Edit
Scaffold(
  appBar: AppBar(
    title: const Text('Traffic Light Game'),
  ),
  body: Center(
    child: Column(
      children: [...],
    ),
  ),
);
It sets up the structure of the game page.

6. setState
Updates the UI whenever a change happens (like tapping a cell).

dart
Copy
Edit
void _handleTap(int row, int col) {
  setState(() {
    grid[row][col] = (grid[row][col] + 1) % 4;
    changeCount[row][col]++;
  });
}
Without setState, Flutter would not redraw the screen after player moves.

7. LinearGradient
Adds a nice background color transition effect.

dart
Copy
Edit
decoration: BoxDecoration(
  gradient: LinearGradient(
    begin: Alignment.topCenter,
    end: Alignment.bottomCenter,
    colors: [
      Theme.of(context).primaryColor.withOpacity(0.1),
      Colors.white,
    ],
  ),
),
It fades the background from a light blue to white vertically.

8. MaterialApp
The root widget that holds settings for your whole app.

dart
Copy
Edit
MaterialApp(
  title: 'Traffic Light Game',
  theme: ThemeData(
    primarySwatch: Colors.blue,
    useMaterial3: true,
  ),
  home: const GameScreen(),
);
It defines:

App title.

Default app theme.

What screen should load first (GameScreen).

📈 Features
4x3 flexible grid system.

Smart win detection (horizontal, vertical, and diagonals).

Beautiful custom painted shapes.

Game reset option.

Clear turn indicators and win messages.

🖼️ UI Highlights
Smooth background gradient.

Light shadow effects around the grid.

Fun and colorful traffic light shapes.

Clear and bold text for players and winner announcement.

💡 Future Improvements
Add a scoring system.

Add timer limits for turns.

Add basic AI for single player mode.

Include sound effects and animations.

📌 Quick Glimpse of Main Methods

Method	Purpose
_handleTap(row, col)	Handles tap events, updates the cell, switches turns.
_resetGame()	Resets the board and starts a new game.
_checkWin(shape)	Checks if any player has won by aligning three same shapes.
_getShape(state)	Returns the correct painted widget for the current state.
🌟 Conclusion
This project demonstrates event-driven programming, custom graphics rendering, and state management in Flutter.
It is perfect for developers learning Flutter’s rendering system and interaction handling through real gameplay.
