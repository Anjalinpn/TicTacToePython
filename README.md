# TicTacToePython
# Global Variables

#presenting game board
board = ["-", "-", "-",
         "-", "-", "-",
         "-", "-", "-",]

#if game is still going
game_still_going = True

#who won or tie?
winner = None

#whose turn it is?
current_player = "X"
def display_board():
    print(board[0] + "|" + board[1] + "|" + board[2])
    print(board[3] + "|" + board[4] + "|" + board[5])
    print(board[6] + "|" + board[7] + "|" + board[8])

def play_game():

 #display initial board
 display_board()
 #while the game is still going on
 while game_still_going:
   #handle a single turn of an arbitrary player
  handle_turn(current_player)
   #check whether the game has ended or not
  check_if_game_over()

  #flip to other player
  flip_player()


 #the game has ended here
 if winner == "X" or winner == "O":
     print(winner + " WON! ")
 elif winner == None:
     print(" It's a Tie! ")

#displaying the board format
def display_board():
    print("\n")
    print(board[0] + " | " + board[1] + " | " + board[2] + "     1 | 2 | 3")
    print(board[3] + " | " + board[4] + " | " + board[5] + "     4 | 5 | 6")
    print(board[6] + " | " + board[7] + " | " + board[8] + "     7 | 8 | 9")
    print("\n")

#handle a single turn of an arbitrary player
def handle_turn(player):

    print(player + "'s turn. ")
    position = input(" Choose a position from 1-9: ")
    valid = False
    while not valid:

     while position not in ["1", "2", "3", "4", "5", "6", "7", "8", "9"]:
        position = input("Invalid input. Choose a position from 1-9: ")
     position = int(position) - 1

     if board[position] == "-":
        valid = True
     else:
        print(" You cant go there. Go again! ")

    board[position] = player

    display_board()

def check_if_game_over():
    check_winner()
    check_if_tie()

def check_winner():
    #for global variables
    global winner

    #checking rows
    row_winner = check_rows()

    #checkimg columns
    column_winner = check_columns()

    #checking diagonals
    diagonal_winner = check_diagonals()
    if row_winner:
        winner = row_winner
    elif column_winner:
        winner = column_winner
    elif diagonal_winner:
        winner = diagonal_winner
    else:
        winner = None
    return

def check_rows():
    global game_still_going
    #check if any of rows have all the same value and not empty
    row_1 = board[0] == board[1] == board[2] != "-"
    row_2 = board[3] == board[4] == board[5] != "-"
    row_3 = board[6] == board[7] == board[8] != "-"
    #If any row does have a match, then there's a win
    if row_1 or row_2 or row_3:
        game_still_going = False
    #return to the winner either X or O
    if row_1:
        return board[0]
    elif row_2:
        return board[3]
    elif row_3:
        return board[6]
    return



def check_columns():
    global game_still_going
    # check if any of columns have all the same value and not empty
    column_1 = board[0] == board[3] == board[6] != "-"
    column_2 = board[1] == board[4] == board[7] != "-"
    column_3 = board[2] == board[5] == board[8] != "-"
    # If any column does have a match, then there's a win
    if column_1 or column_2 or column_3:
        game_still_going = False
    # return to the winner either X or O
    if column_1:
        return board[0]
    elif column_2:
        return board[1]
    elif column_3:
        return board[2]
    return
def check_diagonals():
    global game_still_going
    # check if any of diagonals have all the same value and not empty
    diagonals_1 = board[0] == board[4] == board[8] != "-"
    diagonals_2 = board[6] == board[4] == board[2] != "-"
    # If any diagonal does have a match, then there's a win
    if diagonals_1 or diagonals_2:
        game_still_going = False
    # return to the winner either X or O
    if diagonals_1:
        return board[0]
    elif diagonals_2:
        return board[6]
    return

def check_if_tie():
    global game_still_going
    if"-" not in board:
        game_still_going = False
    return

def flip_player():
    global current_player
    #if current player was X, then change it to O.
    if current_player == "X":
        current_player = "O"
    #if current player was O, then change it to X.
    elif current_player == "O":
        current_player = "X"
    return

play_game()





