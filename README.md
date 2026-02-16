from random import choice

print('Приветствую на игре "Виселица"')

HANGMAN = (
    """
     ------
     |    |
     |
     |
     |
     |
     |
    ----------
    """,
    """
     ------
     |    |
     |    O
     |
     |
     |
     |
    ----------
    """,
    """
     ------
     |    |
     |    O
     |    |
     |
     |
     |
    ----------
    """,
    """
     ------
     |    |
     |    O
     |   /|
     |
     |
     |
    ----------
    """,
    """
     ------
     |    |
     |    O
     |   /|\\
     |
     |
     |
    ----------
    """,
    """
     ------
     |    |
     |    O
     |   /|\\
     |   /
     |
     |
    ----------
    """,
    """
     ------
     |    |
     |    O
     |   /|\\
     |   / \\
     |
     |
    ----------
    """
)

max_wrong = len(HANGMAN) - 1  

WORDS = ('Lavr', 'Slautin', 'vvgy')

word = choice(WORDS).lower()  
so_far = '_' * len(word)
wrong = 0
used = []

while wrong < max_wrong and so_far != word:
    print(HANGMAN[wrong])
    print('\nВы использовали следующие буквы:', ', '.join(used))
    print('\nНа данный момент слово выглядит так:\n', ' '.join(so_far))  

    guess = input('\nВведите букву: ').lower()

    
    if len(guess) != 1 or not guess.isalpha():
        print('Пожалуйста, введите одну букву.')
        continue
    if guess in used:
        print('Вы уже вводили букву', guess)
        continue

    used.append(guess)

    if guess in word:
        print('\nДа! Буква', guess, 'есть в слове.')
        
        new = ''
        for i in range(len(word)):
            if guess == word[i]:
                new += guess
            else:
                new += so_far[i]
        so_far = new
    else:
        print('\nИзвините, буквы', guess, 'нет в слове.')
        wrong += 1


if wrong == max_wrong:
    print(HANGMAN[wrong])  
    print('\nТебя повесили! Загаданное слово было:', word)
else:
    print('\nПоздравляю! Вы угадали слово:', word)
