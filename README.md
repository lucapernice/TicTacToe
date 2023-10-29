# Tic Tac Toe Game Board Class 

This is a Python class named `Board` designed to represent the game board for a Tic Tac Toe game. It provides methods for initializing the board, clearing the board, checking for a win, and inserting symbols (X or O) into the board.

## Class `Board`

### Constructor: `__init__(self)`

The constructor initializes the game board by creating a 3x3 matrix filled with `None` values. It represents the empty state of the board.

### Method: `clear_board(self)`

This method clears the game board by setting all its elements to `None`. It effectively resets the board to its initial empty state, allowing a new game to begin.

### Method: `empty_cells(self)`

This method returns a list of free cells (positions) on the game board. It iterates through the 3x3 matrix and identifies all the cells that are still unoccupied (with a value of `None`). The list of free cells is returned as a list of tuples, each containing the (row, column) position of an empty cell.

### Method: `check_win(self, position)`

This method checks if a player has won the game by placing their symbol (X or O) at a given `position` on the board. It checks for a winning combination in the row, column, or diagonal that includes the specified position.

- If the symbol at the given position is `None`, the method returns `False` as there is no win.
- If the symbol at the given position forms a winning combination in the row, column, or diagonal, the method returns `True`, indicating that the player has won.

### Method: `insert(self, symbol, row, column, print_out=False)`

This method allows a player to insert their symbol (`symbol`) into a specified cell on the game board, determined by the `row` and `column` parameters. It also checks for a win and can print a victory message if `print_out` is set to `True`.

- The `symbol` parameter represents the player's symbol (either 'X' or 'O').
- The `row` parameter represents the row index where the symbol will be placed.
- The `column` parameter represents the column index where the symbol will be placed.
- If the `print_out` parameter is set to `True`, and the player's move results in a win, the method prints a message indicating which player has won.

Please note that this class is designed for use in a Tic Tac Toe game, and it handles the game board's state and checking for wins but does not manage the game's overall flow or player turns. It's meant to be integrated into a larger game framework or used as part of a complete Tic Tac Toe implementation.

# Monte Carlo Tree Search (MCTS) for Tic Tac Toe

The provided code implements the Monte Carlo Tree Search algorithm to find the best move for a given state of the Tic Tac Toe game. This algorithm helps a computer player (symbol 'o') decide its next move by simulating different game scenarios and selecting the move that maximizes the chances of winning. The following documentation describes the code and its components.

## Main Program

The main program implements the MCTS algorithm and provides a way to find the best move for the computer player in a Tic Tac Toe game.

### Function: `best_move(node, max_iterations=1000)`

This function takes a game state as a `Node` object and returns the best move for the computer player ('o') after running a specified number of MCTS iterations.

- `node`: The root node of the search tree, representing the current game state.
- `max_iterations`: The maximum number of MCTS iterations to perform (default is 1000).

## Class `Node`

The `Node` class represents a node in the MCTS search tree. Each node corresponds to a specific game state. The tree is expanded as MCTS iterations are performed, and nodes represent various game states and their possible moves.

### Constructor: `__init__(self, board, parent=None, list_of_child=[], value=0, visited_count=0, player='o')`

- `board`: The game board state represented by the node.
- `parent`: The parent node in the tree (default is `None` for the root node).
- `list_of_child`: A list of child nodes (default is an empty list).
- `value`: The number of wins associated with this node (default is 0).
- `visited_count`: The number of times this node has been visited during MCTS iterations (default is 0).
- `player`: The player associated with this node ('o' for computer player, 'x' for human player, default is 'o').

### Method: `get_actions(self)`

This method returns a list of possible actions (i.e., reachable game states) for the current state of the game. It identifies empty cells on the game board and returns the resulting game states and their corresponding positions.

### Method: `ucb(self, c=math.sqrt(2))`

This method calculates the Upper Confidence Bound (UCB) score for the node, which balances exploration and exploitation. It helps select which child node to explore further during the selection phase of MCTS.

- `c`: A constant parameter that controls the balance between exploration and exploitation (default is the square root of 2).

### Method: `select(self)`

This method selects the next node to explore during the selection phase of MCTS. It uses the UCB score to make this decision and chooses the child node with the highest UCB score. The selection continues until a leaf node is reached.

### Method: `rollout(self)`

This method simulates a random game rollout from the current node until a game-ending condition is met (win, tie, or loss). It returns information about the outcome of the simulation.

### Method: `expand_simulate(self)`

This method is called after selecting a node during the expansion phase of MCTS. It expands the tree by adding child nodes representing possible game moves and then simulates a game rollout from one of the child nodes.

### Method: `single_iteration(self)`

This method represents a single iteration of the MCTS algorithm. It involves selecting a node, expanding the tree, simulating a game, and updating the node's statistics. The results of the game simulation are used to update the statistics for the selected node and its ancestors in the tree.

Please note that the MCTS algorithm is run in the `best_move` function, which repeatedly performs these iterations until a specified number is reached, leading to better-informed decisions about the best move for the computer player in Tic Tac Toe.

The code can be tested by creating a game board, initializing a root node, and running the `best_move` function to find the best move for the computer player in a Tic Tac Toe game.


