# Hangman 

Hangman Game is a fun and interactive console-based game where players try to guess a word by suggesting letters within a limited number of attempts. The game visually displays the number of lives left using a hangman graphic.

## Features:

- Interactive console-based gameplay.
- Visual representation of remaining lives.
- Word guessing with feedback on used letters and current word state.

## Installation:

1. **Clone the repository:**

    ```
    git clone https://github.com/Rafsun07/Hangman.git
    cd hangman
    ```

2. **Run the game:**

    ```
    python hangman.py
    ```
    
## Usage:

1. **Start the game:**

    Run the `hangman.py` script to start the Mad Libs game.

    ```
    python hangman.py
    ```

2. **Input Prompts:**

    The game will prompt you to guess letters. You can guess by typing a letter and pressing Enter. The game will provide feedback on whether the guessed letter is in the word and how many lives you have left.
   
    ### Example interaction
    You have 7 lives left and you have used these letters: A B C
    Current word: - - N - G - A N
    Guess a letter: H

    ### Continue guessing until you either guess the word or run out of lives.
   

## How the Code Works:

The Hangman game code is structured to provide an interactive word-guessing experience in the console. Here's a step-by-step breakdown of how the code works:

### 1. Importing Required Modules:

The code begins by importing necessary modules:

 ```
  import random
  from words import words
  from hangman_visual import lives_visual_dict
  import string
 ``` 
    
- `random`: Used for selecting a random word from the list.
- `words`: A module containing a list of possible words for the game.
- `hangman_visual`: A module containing visual representations of the hangman based on remaining lives.
- `string`: Provides a set of ASCII uppercase letters.

### 2. Selecting a Valid Word:

```
def get_valid_word(words):
    word = random.choice(words)
    while '-' in word or ' ' in word:
        word = random.choice(words)
    return word.upper()
```

- The `get_valid_word` function selects a random word from the words list and ensures it does not contain spaces or hyphens:

### 3. Main Game Logic:

The `hangman` function contains the main logic for the game:

```
def hangman():
    word = get_valid_word(words)
    word_letters = set(word)  # Letters in the word to be guessed
    alphabet = set(string.ascii_uppercase)
    used_letters = set()  # Letters guessed by the user

    lives = 7

    while len(word_letters) > 0 and lives > 0:
        # Display current state
        print('You have', lives, 'lives left and you have used these letters: ', ' '.join(used_letters))
        word_list = [letter if letter in used_letters else '-' for letter in word]
        print(lives_visual_dict[lives])
        print('Current word: ', ' '.join(word_list))

        # Get user input
        user_letter = input('Guess a letter: ').upper()
        if user_letter in alphabet - used_letters:
            used_letters.add(user_letter)
            if user_letter in word_letters:
                word_letters.remove(user_letter)
            else:
                lives -= 1
                print('\nYour letter,', user_letter, 'is not in the word.')
        elif user_letter in used_letters:
            print('\nYou have already used that letter. Guess another letter.')
        else:
            print('\nThat is not a valid letter.')

    # Game over messages
    if lives == 0:
        print(lives_visual_dict[lives])
        print('You died, sorry. The word was', word)
    else:
        print('YAY! You guessed the word', word, '!!')
```

- Initialization: The game starts by selecting a valid word and initializing the sets for word letters, the alphabet, and used letters. The player starts with 7 lives.
- Main Loop: The loop continues until the player has either guessed all the letters in the word or run out of lives.
   - Display State: Shows the number of lives left, the letters used, and the current state of the word.
   - User Input: Prompts the user to guess a letter.
   - Input Validation: Checks if the guessed letter is valid and not already used.
      - If the letter is in the word, it is removed from the set of word letters.
      - If the letter is not in the word, the player loses a life.
- Repeated or Invalid Input: Handles cases where the user inputs a letter they have already guessed or an invalid character.
- Game Over: Displays a message indicating whether the player has won or lost the game.


## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes. Ensure that your code follows the project's coding standards and includes appropriate tests.

## Contact

For questions, suggestions, or issues, please open an issue on GitHub or contact the project maintainer at [rafsun.eram@gmail.com](mailto:rafsun.eram@gmail.com).

## Acknowledgements

- Developed using Python.
- Inspired by a fun and interactive console-based game caleed Hangman.

---
