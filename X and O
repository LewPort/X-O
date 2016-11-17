import random
import sys
import copy
import time

board = {7: ' ', 8: ' ', 9: ' ',
         4: ' ', 5: ' ', 6: ' ',
         1: ' ', 2: ' ', 3: ' '}

human = 'unassigned'
computer = 'X'
turn = 'human'

def chooseLetter(): #Choosing what letter you play as (X or O)
    global human
    global computer
    while human != 'X' and human != 'O':
        human = input('Choose your letter (X or O): ').upper()
    if human == 'X':
        computer = 'O'
    else: computer = 'X'


def printBoard(board): #Prints the board in its current state
    print('\n' + board[7] + '|' + board[8] + '|' + board[9])
    print('-+-+-')
    print(board[4] + '|' + board[5] + '|' + board[6])
    print('-+-+-')
    print(board[1] + '|' + board[2] + '|' + board[3] + '\n')

def resetBoard():
    for i in board:
        board[i] = ' '

def coinToss(): #Tosses a virtual coin to see who goes first
    coinGuess = ''
    while coinGuess != 'H' and coinGuess != 'T':
        coinGuess = input('Choose Heads or Tails to see who goes first (H or T): ').upper()
    if random.randint(0, 1) == 0:
        coinResult = 'H'
    else:
        coinResult = 'T'
    if coinResult == coinGuess:
        print('Yep, it\'s ' + coinResult + '! You go first.')
        return True
    else:
        print('Sorry, it was ' + coinResult + '. Computer goes first!')
        return False
    
def getHumanMove(): #Player inputs their move
    global turn
    turn = 'human'
    humanMoveIndex = int(input('Choose your move (1-9): '))
    while humanMoveIndex not in range(1, 10) or board[humanMoveIndex] != ' ':
        try:
            humanMoveIndex = int(input('Choose your move (1-9): '))
        except ValueError:
            continue   
    board[humanMoveIndex] = human


#AI AI AI AI AI AI AI AI
def getComputerMove():
    global turn
    turn = computer
    tempBoard = copy.copy(board)
    compMoveComplete = False

    print('\nX/0 5000 BOT IS CALCULATING MOVE\nSTAND BY FOR IMPLIMENTATION', end='')
    for i in range(1,11):
        print('.', end = '')
        time.sleep(0.01)
    print('\n')

    #Checks for winning move    
    if compMoveComplete == False:
        print('<<Checking for winning move>>')
        for i in tempBoard: 
            if tempBoard[i] == ' ':
                tempBoard[i] = computer
                if aWinner(tempBoard, computer) == True:
                    print('<<Found winning move at ' + str(board[i]) +'>>')
                    board[i] = computer
                    compMoveComplete = True
                    return
                elif aWinner(tempBoard, computer) == False:
                    tempBoard[i] = ' '

        #Checks to see if computer can block human's winning move           
        print('<<Checking to see if opponent can win next move>>')                   
        for i in tempBoard: 
            if tempBoard[i] == ' ':
                tempBoard[i] = human
                if aWinner(tempBoard, human) == True:
                    print('<<Blocked human\'s winning move at ' + str(i) +'>>')
                    board[i] = computer
                    compMoveComplete = True
                    return
                elif aWinner(tempBoard, human) == False:
                    tempBoard[i] = ' '
                    
          
        #Checks to see if Centre is free
        print('<<Checking centre>>')
        if compMoveComplete == False and board[5] == ' ':
            print('<<Taking centre>>')
            board[5] = computer
            compMoveComplete = True
            return

        elif compMoveComplete == False and ' ' in board[1] or ' ' in board[3] or ' ' in board[7] or ' ' in board[9]:
            print('<<Checking corners>>') #Checks to see if a random corner is free
            corners = [1,3,7,9]
            random.shuffle(corners)
            for i in range(len(corners)):
                print('<<Checking corner ' + str(corners[i]) + '>>')
                if board[corners[i]] == ' ':
                    board[corners[i]] = computer
                    print('<<found and claimed CORNER side at ' + str(corners[i]) + '>>')
                    compMoveComplete=True
                    return
                else:
                    print('<<NO FREE CORNERS FOUND!!!>>')
            print('<<Finished checking Corners>>')
                    
              
        elif compMoveComplete == False and ' ' in board[2] or ' ' in board[4] or ' ' in board[6] or ' ' in board[8]:
            print('<<Checking Sides>>')
            sides = [2, 4, 6, 8] #Checks to see if the side squares are free
            random.shuffle(sides)
            for i in range(len(sides)):
                print('<<Checking side ' + str(sides[i]) + '>>')
                if board[sides[i]] == ' ':
                    board[sides[i]] = computer
                    compMoveComplete=True
                    print('found and claimed free SIDE at ' + str(sides[i]))
                    return
                else:
                    print('NO FREE SIDES FOUND!!!')

def aWinner(board, pl): #Winning combinations
        return ((board[7] == pl and board[8] == pl and board[9] == pl) or
        (board[4] == pl and board[5] == pl and board[6] == pl) or
        (board[1] == pl and board[2] == pl and board[3] == pl) or
        (board[7] == pl and board[4] == pl and board[1] == pl) or
        (board[8] == pl and board[5] == pl and board[2] == pl) or
        (board[9] == pl and board[6] == pl and board[3] == pl) or
        (board[9] == pl and board[5] == pl and board[1] == pl) or
        (board[7] == pl and board[5] == pl and board[3] == pl))

def playAgain():
    playAgain = 'butts'
    while playAgain != 'Y' and playAgain != 'N':
        playAgain = input('Do you want to play again? (Y/N) ').upper()
    if playAgain == 'Y':
        resetBoard()
        human = 'butts'
        computer = 'poop'
    else:
        sys.exit()




#HERE'S THE ACTUAL GAME VVVVVV

while True:
    chooseLetter()
    if coinToss() == True:
        printBoard(board)
        getHumanMove()
        printBoard(board)
        turn = 'computer'
    else:
        getComputerMove()
        turn = 'human'
        
    while aWinner(board, human) == False and aWinner(board, computer) == False:
        if ' ' not in board.values():
            print('DRAW!!!')
            playAgain()
        
        elif turn == 'human':
            printBoard(board)
            getHumanMove()
            printBoard(board)
            turn = 'computer'

        elif turn == 'computer':
            getComputerMove()
            turn = 'human'

    if aWinner(board, human) == True:
        printBoard(board)
        print('CONGRATULATIONS! You win!')
        playAgain()
    elif aWinner(board, computer) == True:
        printBoard(board)
        for i in range(1,20):
            print('X/O 5000 BOT IS VICTORIOUS ONCE AGAIN.')
        playAgain()
        
