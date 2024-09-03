## Step 1 - Printing the Board

**Implement the Board Display Function**

Here's how we create a function to display the game board in the terminal. Each row of the board is represented as a list, and this function prints each list with vertical bars to visually separate the columns.

```
def print_board(board):
    for row in board:
        print("|" + "|".join(row) + "|")

# Test the print_board function:
# print_board([["X", "O", "X"], ["O", "X", "O"], ["X", "O", "X"]])
```

## Step 2 - Handling Player Moves

**Create the Player Input Function**

This function prompts the player to enter their move as 'row,col', checks if the input is valid, and updates the board accordingly. It ensures that moves are made within the bounds of the board and into empty spaces.

```
def player_move(board, player):
    while True:
        try:
            move = input(f"Player {player}, enter your move as 'row,col': ")
            row, col = map(int, move.split(","))
            if (
                row >= 1
                and row <= 3
                and col >= 1
                and col <= 3
                and board[row - 1][col - 1] == " "
            ):
                board[row - 1][col - 1] = player
                break
            else:
                print("Invalid move. Please try again.")
        except ValueError:
            print(
                "Invalid input. Please enter row and column as 'row,col' (e.g., 2,3)."
            )
        except IndexError:
            print("Invalid input. Row and column must be between 1 and 3.")
```

## Step 3 - Determining a Winner

**Implement the Win Condition Check**

This function checks all possible winning combinations (horizontal, vertical, and diagonal) to determine if there is a winner.

```
def check_win(board):
    # Check horizontal, vertical, and diagonal lines for a win
    lines = []
    lines.extend(board)  # horizontal lines
    lines.extend(zip(*board))  # vertical lines
    lines.append([board[i][i] for i in range(3)])  # main diagonal
    lines.append([board[i][2 - i] for i in range(3)])  # secondary diagonal

    for line in lines:
        if line.count(line[0]) == 3 and line[0] != " ":
            return True
    return False
```

## Step 4 - Checking for a Tie

**Add the Tie Condition Function**

This function checks if all spaces on the board are filled without a winner, indicating a tie.

```
def check_tie(board):
    for row in board:
        if " " in row:
            return False
    return True
```

## Step 5 - Main Game Loop

**Define the Main Game Function**

This function initializes the game board, and manages the game flow, alternating between players until a win or tie is detected.

```
def play_game():
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

    while True:
        print_board(board)
        player_move(board, current_player)

        if check_win(board):
            print_board(board)
            print(f"Player {current_player} wins!")
            break
        if check_tie(board):
            print_board(board)
            print("The game is a tie!")
            break

        # Switch player
        current_player = "O" if current_player == "X" else "X"

    print("Game over!")

# Start the game
play_game()
```


