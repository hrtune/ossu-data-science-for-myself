
## Rule

CPU selects a random word and tells the length of the word

Initial prompt
```
Loading word list from file...
55900 words loaded.
Welcome to the game, Hangman!
I am thinking of a word that is 4 letters long.
```

Separator divides each section:
```
-------------
```

Main prompt:
```
You have 8 guesses left.
Available letters: abcdefghijklmnopqrstuvwxyz
Please guess a letter: a
Good guess: _ a_ _
```

First line of main prompt:
```
You have <num> guesses left.
```
- num: initially 8, downs to 1
	- If the guess is incorrect, num decrements by one

Second line of main prompt:
```
Available letters: <available_letters>
```
- available_letters is initially "abcdefghijklmnopqrstuvwxyz"
	- When a user guessed a letter, the letter is removed from the string.

Third line of main prompt:
```
Please guess a letter: <a_character_from_user_input>
```

Fourth line of main prompt:
```
<message>: <letter_board>
```
- `message` is one of:
	- `Good guess`: when user's guess is correct
	- `Oops! You've already guessed that letter`: when user input already guessed letter
	- `Oops! That letter is not in my word`: when failure
- `letter_board` is in the form:
	- Initially `_ _ _ _`
	- A letter with a correct guess replaces `_` at the correct position(s).

Prompt after win:
```
Congratulations, you won!
```

Prompt after lose:
```
Sorry, you ran out of guesses. The word was <correct_word>.
```


## Problem 1 - Is the Word Guesed

```python
def isWordGuessed(secretWord, lettersGuessed):
  '''
  secretWord: string, the word the user is guessing
  lettersGuessed: list, what letters have been guessed so far
  returns: boolean, True if all the letters of secretWord are in lettersGuessed;
    False otherwise
  '''

  for c in set(secretWord):
    if c not in lettersGuessed:
      return False

  return True
```


## Problem 2 - Printing Out the User's Guess
Next, implement the function `getGuessedWord` that takes in two parameters - a string, `secretWord`, and a list of letters, `lettersGuessed`. This function returns a string that is comprised of letters and underscores, based on what letters in `lettersGuessed` are in `secretWord`. This shouldn't be too different from `isWordGuessed`!


```python
def getGuessedWord(secretWord, lettersGuessed):
    '''
    secretWord: string, the word the user is guessing
    lettersGuessed: list, what letters have been guessed so far
    returns: string, comprised of letters and underscores that represents
      what letters in secretWord have been guessed so far.
    '''

    letter_board = []

    for c in secretWord:
      if c in lettersGuessed:
        letter_board.append(c)
      else:
        letter_board.append('_')
    
    return ' '.join(letter_board)
```

## Problem 3 - Printing Out all Available Letters

```python
def getAvailableLetters(lettersGuessed):
  '''
  lettersGuessed: list, what letters have been guessed so far
  returns: string, comprised of letters that represents what letters have not
    yet been guessed.
  '''

  letters = "abcdefghijklmnopqrstuvwxyz"

  for c in lettersGuessed:
    letters = letters.replace(c, '')

  return letters
```

## Problem 4 - The Game

```python
def hangman(secretWord):
  '''
  secretWord: string, the secret word to guess.

  Starts up an interactive game of Hangman.

  * At the start of the game, let the user know how many 
    letters the secretWord contains.

  * Ask the user to supply one guess (i.e. letter) per round.

  * The user should receive feedback immediately after each guess 
    about whether their guess appears in the computers word.

  * After each round, you should also display to the user the 
    partially guessed word so far, as well as letters that the 
    user has not yet guessed.

  Follows the other limitations detailed in the problem write-up.
  '''

  separator = "----------"

  # Initial prompt
  print("Welcome to the game, Hangman!")
  print(f"I am thinking of a word that is {len(secretWord)} letters long.")

  print(separator)

  guesses_left = 8

  letters_guessed = set()



  # Main prompt
  while guesses_left > 0:


    print(f"You have {guesses_left} guesses left")

    available_letters = getAvailableLetters(letters_guessed)
    print(f'Available Letters: {available_letters}')

    guess = input("Please guess a letter: ").lower()

    if guess in letters_guessed:
      message = "Oops! You've already guessed that letter"
    elif guess in secretWord:
      message = "Good guess"
    else:
      message = "Oops! That letter is not in my word"
      guesses_left -= 1

    letters_guessed.add(guess)

    print(f"{message}: {getGuessedWord(secretWord, letters_guessed)}")

    print(separator)

    if isWordGuessed(secretWord, letters_guessed):
      print("Congratulations, you won!")
      return

  print(f"Sorry, you ran out of guesses. The word was {secretWord}.")
```