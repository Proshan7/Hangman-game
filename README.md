# Hangman-game
Hangman is a word-guessing game where the player tries to guess a hidden word one letter at a time. For each incorrect letter guess, a part of a "hangman" drawing (or a remaining guess counter) is lost. The player wins by revealing all letters of the word before running out of allowed wrong guesses; otherwise the player loses.
# Task 1: Hangman Game
import random

def hangman():
    words = {
        "python": "A popular programming language",
        "code": "Something programmers write",
        "game": "What you are playing now",
        "hangman": "The name of this game",
        "keyboard": "Used for typing letters on a computer"
    }

  
    word, hint = random.choice(list(words.items()))
    guessed_letters = []
    attempts = 6
    won = False   

    display = ["_"] * len(word)
    display[0] = word[0]
    display[-1] = word[-1]
    guessed_letters.extend([word[0], word[-1]])

    print("Welcome to Hangman!")
    print("Hint:", hint)
    print(f"The word has {len(word)} letters.")
    print(f"First letter is '{word[0]}' and last letter is '{word[-1]}'.")
    print("Guess the word:", " ".join(display))

    while attempts > 0:
        
        if "_" not in display:
            print("🎉 Congratulations! You guessed the word:", word)
            won = True
            break

        guess = input("Enter a letter (or the whole word): ").lower()

        if len(guess) > 1:
            if guess == word:
                print("🎉 Congratulations! You guessed the word:", word)
                won = True
                break
            else:
                attempts -= 1
                print(f"Wrong word! Attempts left: {attempts}")
                continue

        if guess in guessed_letters:
            print("You already guessed that letter!")
            continue

        guessed_letters.append(guess)

        if guess in word:
            for i in range(len(word)):
                if word[i] == guess:
                    display[i] = guess
            print("Good guess:", " ".join(display))
        else:
            attempts -= 1
            print(f"Wrong guess! Attempts left: {attempts}")
            print("Word so far:", " ".join(display))

        print("Guessed letters so far:", ", ".join(guessed_letters))
    if not won:
        print("💀 Game Over! The word was:", word)



hangman()
