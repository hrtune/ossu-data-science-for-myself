
Letters are dealt to players, who then construct one or more words out of their letters. Each **valid** word receives a score, based on the length of the word and the letters in that word.

## Prompt Analysis

A whole program structure:
```
<loading>
<loop>
	<menu>
	<game>
	<new_line>
</loop>
```


menu:
```
Enter n to deal a new hand, r to replay the last hand, or e to end game: <user_input>
```
- user_input is one of: n, r, and e

A single game:
```
Current Hand: p z u t t t o
Enter word, or a "." to indicate that you are finished: tot
"tot" earned 9 points. Total: 9 points
Current Hand: p z u t
Enter word, or a "." to indicate that you are finished: .
Total score: 9 points.
```

A game structure
```
<loop>
	<current_hand>
	<word_input>
	<score_message>
</loop>
<total_score>
```

current_hand:
```
Current Hand: <hand>
```
- hand is: `* * * ...` space separated characters.

word_input:
```
Enter word, or a "." to indicate that you are finished: <input>
```
- input: word or `.`
- When input is `.`, total_score is shown.
- When word is invalid, score_message(invalid) is shown next.

score_message(valid):
```
"<word>" earned <point> points. Total: <total_point> points
```
- when hand is used up, total_score(run out) is shown next

score_message(invalid):
```
Invalid word, please try again.
```

total_score:
```
Total score: <score> points.
```

total_score(run out):
```
Run out of letters. Total score: 99 points.
```


## Problems (ps4a.py)

getWordScore:
```python
def getWordScore(word, n):

    score = 0
    
    for c in word.lower():
        score += SCRABBLE_LETTER_VALUES[c]
    
    score *= len(word)
    
    if len(word) == n:
        score += 50

    return score
```

updateHand:
```python
def updateHand(hand, word):

    new_hand = hand.copy()
    for c in word:
        new_hand[c] -= 1

    return new_hand
```

isValidWord:
```python
def isValidWord(word, hand, wordList):

    if not word in wordList:
        return False

    word_freq = getFrequencyDict(word)
    for c in word_freq:
        if c not in hand or hand[c] < word_freq[c]:
            return False
    
    return True
```

calculateHandLen:
```python
def calculateHandlen(hand):

    return sum(hand.values())
```

playHand:
```python
def playHand(hand, wordList, n):
    
    # Keep track of the total score
    total_score = 0
    
    # As long as there are still letters left in the hand:
    while calculateHandlen(hand) > 0:
        # Display the hand
        print("Current Hand: ", end="")
        displayHand(hand)

        # Ask user for input
        user_input = input('Enter word, or a "." to indicate that you are finished: ')

        # If the input is a single period:
        if user_input == ".":
            # End the game (break out of the loop)
            print(f"Goodbye! Total score: {total_score} points.")
            break

        # Otherwise (the input is not a single period):
        else:
            # If the word is not valid:
            if not isValidWord(user_input, hand, wordList):
                # Reject invalid word (print a message followed by a blank line)
                print("Invalid word, please try again.\n")
            # Otherwise (the word is valid):
            else:
                # Tell the user how many points the word earned, and the updated total score
                word_score = getWordScore(user_input, n)
                total_score += word_score
                print(f'"{user_input}" earned {word_score} points. Total: {total_score} points.\n')

                # Update the hand
                hand = updateHand(hand, user_input)

    # Game is over (user entered a '.' or ran out of letters), so tell user the total score
    if calculateHandlen(hand) == 0:
        print(f"Run out of letters. Total score: {total_score} points.")
```

playGame:
```python
def playGame(wordList):

    hand = {}

    while True:
        menu = input("Enter n to deal a new hand, r to replay the last hand, or e to end game: ")
        if menu == 'n':
            hand = dealHand(HAND_SIZE)
            playHand(hand, wordList, calculateHandlen(hand))
            print()
        elif menu == 'r':
            if len(hand) == 0:
                print("You have not played a hand yet. Please play a new hand first!")
                print()
                continue
            playHand(hand, wordList, calculateHandlen(hand))
            print()
        elif menu == 'e':
            return
        else:
            print("Invalid command.")
            print()
```

## Problem 7 (ps4b.py)

playGame:
```python
def playGame(wordList):
    
    hand = {}

    while True:
        menu = input("Enter n to deal a new hand, r to replay the last hand, or e to end game: ")

        if menu == 'e':
            return

        if menu == 'n' or menu == 'r':
            if menu == 'n':
                hand = dealHand(HAND_SIZE)
            if menu == 'r' and len(hand) == 0:
                print("You have not played a hand yet. Please play a new hand first!")
                print()
                continue

            print()
            mode = input("Enter u to have yourself play, c to have the computer play: ")

            if mode == 'u':
                playHand(hand, wordList, calculateHandlen(hand))
                print()
            elif mode == 'c':
                compPlayHand(hand, wordList, calculateHandlen(hand))
                print()
            else:
               print("Invalid command.")
               print()
        else:
            print("Invalid command.")
            print()
```