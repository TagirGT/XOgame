# КОЛИЧЕСТВО КЛЕТОК
board_size = 3
# ИГРОВОЕ ПОЛЕ
board = [1,2,3,4,5,6,7,8,9]

def draw_board():
    ''' Выводим игровое поле '''

    print('_' * 4 * board_size)
    for i in range(board_size):
        print((' ' * 3 + '|') * 3)
        print('', board[i * 3], '|', board[1 + i*3],'|', board[2 + i*3], '|')
        print(('_' * 3 + '|') * 3)
#Блок отвечающий за структуру игрового поля выполнен!

def game_step(index, char):
    ''' Выполнение хода '''
    if (index > 9 or index < 1 or board[index-1] in ('X', 'O')):
        return  False
    board[index-1] = char
    return True

def check_win():
    '''Проверяем победу одного игрока'''
    win = False

    win_combo = (
        (0,1,2), (3,4,5), (6,7,8), #Горизонтальные линии
        (0,3,6), (1,4,7), (2,5,8), #Вертикальные линии
        (0,4,8), (2,4,6) #Диагональные линии
    )

    for pos in win_combo:
        if (board [pos[0]] == board[pos[1]] and board [pos[1]] == board[pos[2]] ):
            win = board [pos[0]]


    return win

def trigger_game():
    # текущий игрок
    current_player = "X"
    #номер шага
    step = 1
    draw_board()

    while (step<10) and (check_win() == False):
        index = input("Ход игрока " + current_player + ' Введите номер поля (0 - Выход):')

        if (index == '0'):
            break


        if (game_step(int(index), current_player)):
            print('Удачный ход')

            if (current_player == 'X'):
                current_player = 'O'
            else:
                current_player = 'X'


            draw_board()
            step += 1


        else:
            print("Неверный номер! Повторите!")


    if (step == 10):
        print('Игра окончена. Ничья!')
    else:
        print('Выиграл ' + check_win())


print("Начнем же игру!")
trigger_game()

