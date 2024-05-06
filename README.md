from tkinter import *
from tkinter import ttk

root = Tk()
root.title("Tic Tac Toe")
root.resizable(0, 0)

# Calculate the center position of the screen
screen_width = root.winfo_screenwidth()
screen_height = root.winfo_screenheight()
window_width = 330
window_height = 550
x_position = (screen_width - window_width) // 2
y_position = (screen_height - window_height) // 2

# Set the window position
root.geometry(f"330x550+{x_position}+{y_position}")

frame1 = Frame(root, bg="yellow")
frame1.pack()

titleLabel = Label(
    frame1,
    text="Tic Tac Toe",
    font=("Arial", 26, "bold"),
    bg="yellow",
    width=16,
)
titleLabel.grid(row=0, column=0)

frame2 = Frame(root, bg="pink")
frame2.pack()

board = {
    1: " ",
    2: " ",
    3: " ",
    4: " ",
    5: " ",
    6: " ",
    7: " ",
    8: " ",
    9: " ",
}

turn = "x"
game_end = False

def updateBoard():
    for key in board.keys():
        buttons[key - 1]["text"] = board[key]

def checkForWin(player):
    # rows
    if (
        board[1] == board[2]
        and board[2] == board[3]
        and board[3] == player
    ):
        return True
    elif (
        board[4] == board[5]
        and board[5] == board[6]
        and board[6] == player
    ):
        return True
    elif (
        board[7] == board[8]
        and board[8] == board[9]
        and board[9] == player
    ):
        return True
    # columns
    elif (
        board[1] == board[4]
        and board[4] == board[7]
        and board[7] == player
    ):
        return True
    elif (
        board[2] == board[5]
        and board[5] == board[8]
        and board[8] == player
    ):
        return True
    elif (
        board[3] == board[6]
        and board[6] == board[9]
        and board[9] == player
    ):
        return True
    # diagonals
    elif (
        board[1] == board[5]
        and board[5] == board[9]
        and board[9] == player
    ):
        return True
    elif (
        board[3] == board[5]
        and board[5] == board[7]
        and board[7] == player
    ):
        return True

    return False

def checkForDraw():
    for i in board.keys():
        if board[i] == " ":
            return False

    return True

def restartGame():
    global game_end, turn
    game_end = False
    turn = "x"
    for button in buttons:
        button["text"] = " "

    for i in board.keys():
        board[i] = " "

    for widget in frame1.winfo_children():
        widget.destroy()
    titleLabel.config(
        text="Tic Tac Toe", font=("Arial", 26, "bold"), bg="yellow", width=16
    )


def play(event):
    global turn, game_end
    if game_end:
        return

    button = event.widget
    buttonText = str(button)
    clicked = buttonText[-1]
    if clicked == "n":
        clicked = 1
    else:
        clicked = int(clicked)

    if button["text"] == " ":
        # Update the board with the current player's symbol
        board[clicked] = turn
        updateBoard()

        # Check for win or draw after the current move
        if checkForWin(turn):
            winningLabel = Label(
                frame1,
                text=f"{turn} wins the game",
                bg="yellow",
                font=("Arial", 26),
                width=16,
            )
            winningLabel.grid(
                row=0, column=0, columnspan=3
            )
            game_end = True
        elif checkForDraw():
            drawLabel = Label(
                frame1, text=f"Game Draw", bg="yellow", font=("Arial", 26), width=16
            )
            drawLabel.grid(row=0, column=0, columnspan=3)
            game_end = True
        else:
            # Alternate the turn between players for multiplayer mode
            turn = "o" if turn == "x" else "x"

    else:
        # If the clicked button is already filled, do nothing
        return

style = ttk.Style()
style.configure(
    "LightBlue.TButton",
    background="light blue",
    width=5,
    height=2,
)

button1 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button1.grid(row=0, column=0)
button1.bind("<Button-1>", play)

button2 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button2.grid(row=0, column=1)
button2.bind("<Button-1>", play)

button3 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button3.grid(row=0, column=2)
button3.bind("<Button-1>", play)

button4 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button4.grid(row=1, column=0)
button4.bind("<Button-1>", play)

button5 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button5.grid(row=1, column=1)
button5.bind("<Button-1>", play)

button6 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button6.grid(row=1, column=2)
button6.bind("<Button-1>", play)

button7 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button7.grid(row=2, column=0)
button7.bind("<Button-1>", play)

button8 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button8.grid(row=2, column=1)
button8.bind("<Button-1>", play)

button9 = ttk.Button(
    frame2,
    text=" ",
    width=7,
    style="LightBlue.TButton",
)
button9.grid(row=2, column=2)
button9.bind("<Button-1>", play)

restartButton = ttk.Button(
    frame2,
    text="Restart Game",
    width=19,
    style="TButton",
    command=restartGame,
)
restartButton.grid(row=4, column=0, columnspan=3)

buttons = [
    button1,
    button2,
    button3,
    button4,
    button5,
    button6,
    button7,
    button8,
    button9,
]

root.mainloop()
