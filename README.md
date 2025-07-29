# Two-Player-game
Two-Player Tic Tac Toe game

def print_board(board):
    """Print the current state of the board."""
    print()
    for row in board:
        print(" | ".join(row))      # Show each row with vertical dividers
        print("-" * 9)              # Add a line between rows
    print()

def check_winner(board, player):
    """Check if the given player has won."""
    # Check rows and columns
    for i in range(3):
        if all(cell == player for cell in board[i]):  # All cells in the row match
            return True
        if all(board[j][i] == player for j in range(3)):  # All cells in the column match
            return True

    # Check diagonals
    if all(board[i][i] == player for i in range(3)):      # Top-left to bottom-right
        return True
    if all(board[i][2 - i] == player for i in range(3)):  # Top-right to bottom-left
        return True

    return False  # No win detected

def is_full(board):
    """Check if the board is completely filled."""
    return all(cell in ['X', 'O'] for row in board for cell in row)

def play_game():
    """Main game loop."""
    # Create the board with numbered positions
    board = [
        ['1', '2', '3'],
        ['4', '5', '6'],
        ['7', '8', '9']
    ]

    # Start with player 'X'
    current_player = 'X'

    while True:
        print_board(board)

        # Ask for player's move
        move = input(f"Player {current_player}, choose a cell (1-9): ")

        # Basic input check
        if move not in '123456789':
            print("⛔ Not a valid number between 1 and 9. Try again.")
            continue

        # Convert move to board coordinates
        row = (int(move) - 1) // 3
        col = (int(move) - 1) % 3

        # Check if the spot is already taken
        if board[row][col] in ['X', 'O']:
            print("🚫 That spot is already taken. Try another one.")
            continue

        # Place the player's mark
        board[row][col] = current_player

        # Check if the current player won
        if check_winner(board, current_player):
            print_board(board)
            print(f"🎉 Player {current_player} wins! Congrats!")
            break

        # Check for a draw
        if is_full(board):
            print_board(board)
            print("🤝 It's a draw! No more moves left.")
            break

        # Switch turns
        current_player = 'O' if current_player == 'X' else 'X'

# Run the game
if __name__ == "__main__":
    play_game()
