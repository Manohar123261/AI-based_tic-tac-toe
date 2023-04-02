<!-- # AI-based_tic-tac-toe
I develoved it in tkinter by using python language.
this is advance_tic-tac-toe  branch

--code is here-- -->

from tkinter import *
import random
from time import time,sleep
# global player
def computer():
    global player,flag
    r=random.randint(0,2)
    c=random.randint(0,2)
    if player==players[1] and buttons[r][c]["text"]=="":
        sleep(0.05)
        buttons[r][c]["text"]=players[1]
        if check_winner() is False:
            label.config(text=(players[0]+"   turn"))
            player=players[0]
        elif check_winner()is True:
            label.config(text=(players[1]+"  wins"))
            flag=True
            # for row in range(3):
            #     for col in range(3):
        elif check_winner() is "tie":
            label.config(text=("Tie"))
            for row in range(3):
                for col in range(3):
                    buttons[row][col].config(bg="yellow")
    else:
        computer()
    return player
def prnt(row,col):
    global player,flag
    if  buttons[row][col]["text"]=="":
        buttons[row][col]["text"]=players[0]
        if check_winner() is False:
            label.config(text=(players[1]+"   turn"))
            player=players[1]
            player=computer()
        elif check_winner()is True and flag is not True:
            label.config(text=(players[0]+"  wins"))
            
        elif flag is not True:
            label.config(text=("Tie"))
            for row in range(3):
                for col in range(3):
                    buttons[row][col].config(bg="yellow")


def check_winner():
    if buttons[0][0]["text"]==player and buttons[0][1]["text"]==player and buttons[0][2]["text"]==player:
        buttons[0][0].config(bg="green")
        buttons[0][1].config(bg="green")
        buttons[0][2].config(bg="green")
        return True
    elif buttons[1][0]["text"]==player and buttons[1][1]["text"]==player and buttons[1][2]["text"]==player:
        buttons[1][0].config(bg="green")
        buttons[1][1].config(bg="green")
        buttons[1][2].config(bg="green")
        return True
    elif buttons[2][0]["text"]==player and buttons[2][1]["text"]==player and buttons[2][2]["text"]==player:
        buttons[2][0].config(bg="green")
        buttons[2][1].config(bg="green")
        buttons[2][2].config(bg="green")
        return True
    if buttons[0][0]["text"]==player and buttons[1][0]["text"]==player and buttons[2][0]["text"]==player:
        buttons[0][0].config(bg="green")
        buttons[1][0].config(bg="green")
        buttons[2][0].config(bg="green")
        return True
    elif buttons[0][1]["text"]==player and buttons[1][1]["text"]==player and buttons[2][1]["text"]==player:
        buttons[0][1].config(bg="green")
        buttons[1][1].config(bg="green")
        buttons[2][1].config(bg="green")
        return True
    elif buttons[0][2]["text"]==player and buttons[1][2]["text"]==player and buttons[2][2]["text"]==player:
        buttons[0][2].config(bg="green")
        buttons[1][2].config(bg="green")
        buttons[2][2].config(bg="green")
        return True
    elif buttons[0][0]["text"]==player and buttons[1][1]["text"]==player and buttons[2][2]["text"]==player:
        buttons[0][0].config(bg="green")
        buttons[1][1].config(bg="green")
        buttons[2][2].config(bg="green")
        return True
    elif buttons[0][2]["text"]==player and buttons[1][1]["text"]==player and buttons[2][0]["text"]==player:
        buttons[0][2].config(bg="green")
        buttons[1][1].config(bg="green")
        buttons[2][0].config(bg="green")
        return True
    elif isempty() is False:
        return "tie"
    else:
        return False
def isempty():
    for row in range(3):
        for col in range(3):
            if buttons[row][col]["text"]=="":
                return True
    return False
def new_game():  
    global player,flag
    flag=False
    player=random.choice(players)
    label.config(text=(player+"    turn"))
    for row in range(3):
        for col in range(3):
            buttons[row][col]["text"]=""
            buttons[row][col].config(bg="#F0F0F0")
    if player=="c":
        computer()
root=Tk()
root.title("tic-tac-toe")
players=["x","c"]
player=random.choice(players)
label=Label(root,text=player+"    turn",font="Arial 14 bold")
label.pack()
reset=Button(root,text="restart",command=new_game,font="Arial 14 bold",fg="red")
reset.pack()
buttons=[[0,0,0],
         [0,0,0],
         [0,0,0]]
frame=Frame(root)
frame.pack()
flag=False
for row in range(3):
    for col in range(3):
        buttons[row][col]=Button(frame,text="",command=lambda row=row,col=col:prnt(row,col),font="Arial 14 bold",fg="red",height=4,width=5)
        buttons[row][col].grid(row=row,column=col)
if player=="c":
    computer()
root.mainloop()