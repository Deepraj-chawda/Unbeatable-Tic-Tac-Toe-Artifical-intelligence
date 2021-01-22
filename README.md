# Unbeatable-Tic-Tac-Toe-Artifical-intelligence using Minimax Algorithm in python by Deepraj Chawda .


import time
import os
PLAY=''
COM=''
start=0
end=0
board = [' ',' ',' ',' ',' ',' ',' ',' ',' ']

#This will make a template of tic tac toe

def make_board(b) :
    print("------------------------")
    print("|      |       |       |")
    print("|   "+ b[0] +"  |   "+b[1]+"   |  "+b[2]+"    |")
    print("|      |       |       |")
    print("|      |       |       |")
    print("|----------------------|")
    print("|      |       |       |")
    print("|   "+ b[3] +"  |   "+b[4]+"   |  "+b[5]+"    |")
    print("|      |       |       |")
    print("|      |       |       |")
    print("|----------------------|")
    print("|      |       |       |")
    print("|   "+ b[6] +"  |   "+b[7]+"   |  "+b[8]+"    |")
    print("|      |       |       |")
    print("|      |       |       |")
    print("------------------------")



#This function check winner
#if computer wins it return 1 or if human wins it return -1 else 
#it return 0 for draw or game over

def wins(data) :   
       if ( (data[0]==data[1]==data[2]==COM) or (data[3]==data[4]==data[5]==COM) or (data[6]==data[7]==data[8]==COM) or 
             (data[0]==data[3]==data[6]==COM) or (data[1]==data[4]==data[7]==COM) or (data[2]==data[5]==data[8]==COM) or 
             (data[0]==data[4]==data[8]==COM)  or (data[2]==data[4]==data[6]==COM) ) :
            return 1
        elif ( (data[0]==data[1]==data[2]==PLAY) or (data[3]==data[4]==data[5]==PLAY) or (data[6]==data[7]==data[8]==PLAY) or 
               (data[0]==data[3]==data[6]==PLAY) or (data[1]==data[4]==data[7]==PLAY) or (data[2]==data[5]==data[8]==PLAY) or 
               (data[0]==data[4]==data[8]==PLAY)  or (data[2]==data[4]==data[6]==PLAY) ) :             
            return -1       
        elif " " not in data :
            return 0    
        return 0
        
        
        

#This function check whether board is empty or not
def isempty(my_board) :
    if " " in my_board:
        return True
    return False

#This function is used to clear screen

def clear() :
    if os.name == 'nt' :  #for Windows
        os.system('cls')
    else :               #for Linux
        os.system('clear')
 
#This is min_max_algorithm

def min_max(board,max_play) :
    score = wins(board)                         # three base condition to stop recursion
    if wins(board) == 1 :                    # if computer wins 
        return score 
    if wins(board) == -1 :                   # if human wins
        return score 
    if isempty(board) == False :              # if game over or draw
        return 0 
    if max_play :
        best = -10000
        for i in range(9) :
            if board[i] == " " :
                board[i] = COM
                best = max(best,min_max(board,False))
                board[i] = " "   
        return best                  
    else :
        best = 10000
        for i in range(9) :
            if board[i] == " " :
                board[i] = PLAY
                best = min(best,min_max(board,True))
                board[i] = " "
        return best

# This function gives best move for AI

 def bestmove(board) : 
    best=-1000
    move=-1                                
    for i in range(9) :  
        if board[i] == " " :  #check all the vaild position
            board[i] = COM
            move_val = min_max(board,False)
            board[i] = " "          
            if (move_val > best) :
                move=i
                best=move_val         
    return move
 
 def computer() :  
    global start,end
    start=time.time() 
#For calculating time taken by computer
    best_move= bestmove(board)
    board[best_move] = COM
    end=time.time()
 
#this is main function 

def main() : 
    print('" WELCOME "'.center(90))
    print('"UNBEATABLE AI"'.center(90))
    print('"TIC TAC TOE BY DEEPRAJ"'.center(90))
    #print template of board for user understanding
    make_board(['1','2','3','4','5','6','7','8','9'])
    global COM,PLAY,board
    play_1=input("Enter player  Name : ")
    choice=input(f"{play_1} Enter your choice 'x' or 'O' : ")
    if choice.upper() == 'X' :
        PLAY = "X"
        COM = "O"
    else :
        PLAY = "O"
        COM = "X"  
    print()    
    print(f"{play_1} choice is {PLAY}".center(40))
    print(f"COMPUTER choice is {COM}".center(40))
    first=input('\nDo you want to start first [Y| N] : ')
    if first.upper() =='Y' :
        hum=True
    else :    
        hum=False
flag=0
    while(flag==0) :
        if hum :
            pos=int(input("\n\nEnter a position (1 - 9): "))-1
            if board[pos] == ' ' :
                board[pos] = PLAY
                hum=False
                clear()            
            else :
                clear()
                print("\n\nEnter VALID POSITION !!!!")
        else :
            computer()
            hum=True
            time.sleep(1.5) #stop for 1.5 sec to see human chance 
            clear()
            print("\nTime taken by computer {:.40f} sec\n".format(end-start))
        print('\n')
        make_board(board) 
if wins(board) == 1 :
            print("COMPUTER WINS !!!!".center(80))
            flag=1
            break
        if wins(board) == -1 :
            print(f"{play_1} WINS !!!!".center(80))
            flag=1
            break
        if isempty(board) == False :
            print("Draw !!!!".center(80))
            flag=1
            break           
    while(flag==1):
        ask=input("\nDo you want to continue [Y|N] : ")
        if ask.upper() == 'Y' :
            board = [' ',' ',' ',' ',' ',' ',' ',' ',' ']
            clear()
            main()
        else :
            flag=2
            break
main()

