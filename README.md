# TicTacToe
>TicTacToe game designed in python


**The following grid is used to get player input**
```python
---------------------------
 |       |       |       |
 |   1   |   2   |   3   |
 |       |       |       |
---------------------------
 |       |       |       |
 |   4   |   5   |   6   |
 |       |       |       |
---------------------------
 |       |       |       |
 |   7   |   8   |   9   |
 |       |       |       |
---------------------------
Player 1: Enter the location you want to play
```

*The entered location replaces the number with the players symbol*

**The game ends when the one of the players has won.
The console then gives you an option to start a new game**

```python
---------------------------
 |       |       |       |
 |   X   |   O   |   3   |
 |       |       |       |
---------------------------
 |       |       |       |
 |   4   |   X   |   6   |
 |       |       |       |
---------------------------
 |       |       |       |
 |   O   |   8   |   X   |   
 |       |       |       |
---------------------------
Player 1 has won
Do you want to play again
```

```python
game=[1,2,3,4,5,6,7,8,9]
playerno='Player 1'
def invert(x): #temporarily inverts the player name i use it when print the name of player 
    if x=='Player 1':
        return 'Player 2'
    else:
        return 'Player 1'

def win(game):

    if (game[0]==game[4] and game[4]==game[8]) or (game[2]==game[6]and game[4]==game[6]):
        print(f'{invert(playerno)} has won')
        return True
    elif(game[0]==game[3] and game[3]==game[6]) or (game[1]==game[4] and game[4]==game[7]) or (game[2]==game[5] and game[5]==game[9]):
        print(f'{invert(playerno)} has won')
        return True
    elif(game[0]==game[1] and game[1]==game[2]) or (game[3]==game[4] and game[4]==game[5]) or (game[6]==game[7] and game[7]==game[8]):
        print(f'{invert(playerno)} has won')
        return True

        


def board(token=None,position=None):  #takes care of printing and inserting elements4
    global game
    flag=True
    
    for i in range(len(game)):
        if (game[i]=='O' or game[i]=='X') and i+1==position:    #checks if position is free
            if game[i]==token:
                print(f'That position is taken by {playerno}')  #displys error if position is taken
                return False
            else:
                print(f'That position is taken by {invert(playerno)}')
                return False
        elif game[i]==position:          #inserts into position if available
            game[i]=token
            break
            
        
#prints the board
    print('---------------------------')
    print(' |      ','|       |','      |   ')
    print(f' |   {game[0]}  ',f'|   {game[1]}   |',f'  {game[2]}   |')
    print(' |      ','|       |','      |   ')
    print('---------------------------')
    print(' |      ','|       |','      |   ')
    print(f' |   {game[3]}  ',f'|   {game[4]}   |',f'  {game[5]}   |   ')
    print(' |      ','|       |','      |   ')
    print('---------------------------')
    print(' |      ','|       |','      |   ')
    print(f' |   {game[6]}  ',f'|   {game[7]}   |',f'  {game[8]}   |   ')
    print(' |      ','|       |','      |   ')
    print('---------------------------')

    return flag

def play(token):
    global playerno,game
    if win(game)==True:
        print('Do you want to play again')
        check=input()
        if(check=='y') or (check=='yes'):
            game=[1,2,3,4,5,6,7,8,9]
            playerno='Player 1'
            check='None'
            start()            
        else:
            print('Aww you suck')
            return None
    print(f'{playerno}: Enter the location you want to play')
    location=int(input())       #takes position as an input


    if token=='x' or token=='X':
        token='X'
        if board(token,location)==True:     #Check if Token X has been inserted succesfully
            pass
        else:
            play('X')                       #if insertion has failed calling play  with the same player and token

        if playerno=='Player 1':             #next iteration of the game by inverting playername and token
            playerno='Player 2'
            token='O'
            play(token)
        elif playerno=='Player 2':
            playerno='Player 1'
            token='O'
            play(token)

    elif token=='o'or token=='O':       
        token='O'
        if board(token,location)==True:     #Check if Token O has been inserted succesfully
            pass
        else:
            pass
            play('O')                   #if insertion has failed calling play  with the same player and token
        if playerno=='Player 1':
            playerno='Player 2'
            token='X'
            play(token)
        elif playerno=='Player 2':
            playerno='Player 1'
            token='X'
            play(token)




def start():
    print('Welcome to Tic Tac toe')
    print('Player 1:Do you want to be X or O  ',end='')
    token=input()
    print('Player 1 will go first')
    print('Are you ready to play? Enter Y on N')
    confirm=input()
    if confirm=='Y'or'y':
        board()
        play(token)


start()
```
