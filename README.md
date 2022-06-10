import random
import math
from unittest import result

def play():
    user = input("What is your choice? 'r' for rock, 'p' for paper, 's' for scissors\n")
    user = user.lower()

    computer = random.choice(['r', 'p', 's'])

    if user == computer:
        return (0, user, computer)

    # r > s, s > p, p > r
    if is_win(user, computer):
        return (1, user, computer)

    return (-1, user, computer)

def is_win(player, opponent):
    # return true is the player beats the opponent
    # winning conditions: r > s, s > p, p > r
    if (player == 'r' and opponent == 's') or (player == 's' and opponent == 'p') or (player == 'p' and opponent == 'r'):
        return True
    return False

def play_best_of(n):
    # player against the computer untill someon wins best of n games
    # to win, you must win ceil(n/2) games (ie 2/3, 3/3, 3/5, 4/7)
    player_wins = 0
    computer_wins = 0
    wins_necessary = math.ceil(n/2)
    while player_wins < wins_necessary and computer_wins < wins_necessary:
        result, user, computer = play()
        #tie
        if result ==0:
            print('!TIE! you and computer chose {}. try again.\n'.format(user))
        # you win
        elif result == 1:
            player_wins += 1
            print('!YOU WIN!you chose {} computer chose {} .\n'.format(user, computer))
            # you lose
        elif result == 1:
            player_wins += 1
            print('you lose. you chose {} computer chose {} .\n'.format(user, computer))
        print('\n')

    if player_wins > computer_wins:
        print('!YOU WIN! best of {} Xp' .format(n))
    else:
        print('you lose {} oof:(' .format(n))

if __name__ == '__main__':
    play_best_of(3) # 2
    play_best_of(9) # 5
