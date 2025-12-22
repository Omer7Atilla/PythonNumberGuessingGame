import random

number_string = {0: "Zero", 1: "One", 2: "Two", 3: "Three", 4: "Four", 5: "Five", 6: "Six", 7: "Seven", 8: "Eight",
                 9: "Nine"}

order_string = {1: "First", 2: "Second", 3: "Third", 4: "Fourth", 5: "Fifth", 6: "Sixth"}

def generate_number():
    digits = random.sample(range(10), 5)
    return digits


def player_guess(tries):
    guess = []
    for i in range(5):
        while True:
            digit_input = input(f"Enter digit_{i + 1}=> ")
            if digit_input.isdigit():
                digit = int(digit_input)
                if 0 <= digit <= 9:
                    guess.append(digit)
                    break
                else:
                    print("Please enter a number between 0 and 9")
            else:
                print("Please enter a number between 0 and 9")
    print(f"Your {order_string[tries]} Guess is:",','.join(map(str,guess)))
    return guess


def check(number, guess):
    check_list = []
    for i in range(5):
        if number[i] == guess[i]:
            check_list.append(str(guess[i]))
        elif guess[i] in number:
            check_list.append(number_string[guess[i]])
        else:
            check_list.append("X")
    print(check_list)


def numbrle():
    while True:
        tries = 1
        number = generate_number()
        while tries <= 6:
            guess = player_guess(tries)
            check(number, guess)
            if number == guess:
                print(f"Congratulations you correctly guessed the number after {tries} {'tries' if tries > 1 else 'try'}.")
                answer = input("Do you want to play again? 'Y'/'else'=> ").upper()
                if answer == 'Y':
                    print("Game restarts")
                    number = generate_number()
                    tries = 1
                    continue
                elif answer != 'Y':
                    return
            elif tries == 6:
                print("Game over. You couldn't guess the number in 6 tries.")
                answer = input("Do you want to play again? 'Y'/'else'=> ").upper()
                if answer == 'Y':
                    print("Game restarts")
                    number = generate_number()
                    tries = 1
                    continue
                elif answer != 'Y':
                    return
            else:
                tries += 1
                print("Try again")


numbrle()