# tic-tac-toe.py
Proyecto final del curso(Cisco Networking Academy)

juego_activo = True      
board = [
    ['1', '2', '3'],
    ['4', '5', '6'],
    ['7', '8', '9']
    ]
from random import randrange
def display_board(board):
   for fila in board:
    print("+-------" * 3 + "+")
    linea = "|"
    for celda in fila:
       linea += "   " + celda + "   |"
    print(linea)
    print("|       |       |       |")       
   print("+-------" * 3 + "+")
    

def enter_move(board):
   
    while True:
        try:
            move = int(input("Ingresa tu movimiento (1-9): "))
        except ValueError:
            print("Debes ingresar un número.")
            continue

        if move < 1 or move > 9:
            print("El número debe estar entre 1 y 9.")
            continue
        row = (move - 1) // 3
        col = (move - 1) % 3

        if board[row][col] in ['X', 'O']:
            print("Esa casilla ya está ocupada. Intenta otra.")
            continue
        
        board[row][col] = 'O'
        break
        

def make_list_of_free_fields(board):
     part_empty=[]
     for i in range (len(board)):
        for j in range (len(board[i])):          # La lista esta compuesta por tuplas, cada tupla es un par de números que indican la fila y columna.
         if board[i][j] not in ['X', 'O']:
          part_empty.append((i,j))
    
     return part_empty
   
def victory_for(board, sign):
     
    #filas
     for i in range(3):
        if board[i][0] == sign and board[i][1] == sign and board[i][2] == sign:
            return True

    # columnas
     for j in range(3):
        if board[0][j] == sign and board[1][j] == sign and board[2][j] == sign:
            return True

    # diagonales
     if board[0][0] == sign and board[1][1] == sign and board[2][2] == sign:
        return True

     if board[0][2] == sign and board[1][1] == sign and board[2][0] == sign:
        return True

     return False

                    
def draw_move(board):
    
     free_fields = make_list_of_free_fields(board)
     if len(free_fields) > 0:
        choice = randrange(len(free_fields))
        row, col = free_fields[choice]
        board[row][col] = 'X'
  

while juego_activo:
    display_board(board)
    enter_move(board)
    if victory_for(board, 'O'):
        display_board(board)
        print("¡Felicidades! Has ganado.")
        break
    if not make_list_of_free_fields(board):
        display_board(board)
        print("¡Empate!")
        break
    draw_move(board)
    if victory_for(board, 'X'):
        display_board(board)
        print("La computadora ha ganado.")
        break
    if not make_list_of_free_fields(board):
        display_board(board)
        print("¡Empate!")
        break
    
   

     
   
