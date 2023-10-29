# Tic Tac Toe Strategy and AI

## Introduction

Welcome to the world of Tic Tac Toe, where we explore strategic decision-making and advanced game-playing AI. This repository provides a comprehensive set of Python scripts and modules that empower the computer player ('o') to understand the game state, make intelligent moves, and compete effectively against the human player ('x').

## Code Components

### Code 1: `game.py` - The Tic Tac Toe Game Board Class

In the `game.py` module, we introduce the foundational building block of our Tic Tac Toe game - the `Board` class. This class represents the game board and provides essential methods for managing the game state:

- **Constructor: `__init__(self)`** - Initializes the game board with a 3x3 matrix, where each cell is initially set to `None`, indicating an empty cell.

- **Method: `clear_board(self)`** - Clears the board, effectively restarting the game by resetting all elements to `None`.

- **Method: `empty_cells(self)`** - Identifies and returns a list of empty cells (positions) on the game board.

- **Method: `check_win(self, position)`** - Checks for a winning combination in the row, column, or diagonal that includes the given position and returns `True` if a player has won.

- **Method: `insert(self, symbol, row, column, print_out=False)`** - Allows a player to place their symbol ('X' or 'O') on the board and checks for a win. If `print_out` is set to `True`, it prints a victory message if a win is detected.

### Code 2: `mcts.py` - Monte Carlo Tree Search for Tic Tac Toe

In the `mcts.py` module, we implement the powerful Monte Carlo Tree Search (MCTS) algorithm customized for our Tic Tac Toe game. This algorithm allows the computer player to simulate game rollouts, explore potential moves, and select the best move based on informed choices. It revolves around the `Node` class, which enables advanced decision-making:

- **Class: `Node`** - Represents nodes in the search tree, each corresponding to a game state.

  - **Constructor: `__init__(self, board, parent=None, list_of_child=[], value=0, visited_count=0, player='o')** - Initializes a node with the game board state, parent node (if any), child nodes, value (wins), visited count, and player ('o' for the computer player, 'x' for the human player).

  - **Method: `get_actions(self)`** - Returns a list of possible actions (game states) for the current state. It identifies empty cells on the board, creates new game states for each possible move, and returns the states along with their positions.

  - **Method: `ucb(self, c=math.sqrt(2))`** - Calculates the Upper Confidence Bound (UCB) score for the node, balancing exploration and exploitation.

  - **Method: `select(self)`** - Selects the next node to explore during the selection phase of MCTS. It uses the UCB score to choose the child node with the highest UCB score. The selection continues until a leaf node is reached.

  - **Method: `rollout(self)`** - Simulates a random game rollout from the current node until a game-ending condition (win, tie, or loss) is met. It returns information about the outcome of the simulation.

  - **Method: `expand_simulate(self)`** - Expands the tree by adding child nodes representing possible game moves and then simulates a game rollout from one of the child nodes.

  - **Method: `single_iteration(self)`** - Represents a single iteration of the MCTS algorithm, including selecting a node, expanding the tree, simulating a game, and updating the node's statistics.

- **Function: `best_move(node, max_iterations=1000)`** - Takes a game state node and returns the best move for the computer player ('o') after running a specified number of MCTS iterations. The selected move and its evaluation value are returned.

### Code 3: `limited_depth_search.py` - Limited Depth Search for Tic Tac Toe

The `limited_depth_search.py` script is a modification of the MCTS algorithm called Limited Depth Search (LDS), tailored for Tic Tac Toe. It narrows the search to focus on a limited depth of game states and enhances decision-making. The `lds_node` class extends MCTS and offers the following:

- **Class: `lds_node` (Extends `Node` from `mcts.py)`** - Represents nodes in the search tree, customized for LDS.

  - **Constructor: `__init__(self, board, parent=None, list_of_child=[], value=0, visited_count=0, player='o', depth=0)`** - Initializes a node

