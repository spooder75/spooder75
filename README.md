#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

void displayBoard(std::string secretWord, std::vector<char> guessedLetters, int mistakesMade) {
    std::cout << "Secret word: ";
    for (char c : secretWord) {
        if (std::find(guessedLetters.begin(), guessedLetters.end(), c) != guessedLetters.end()) {
            std::cout << c << " ";
        } else {
            std::cout << "_ ";
        }
    }
    std::cout << std::endl;
    std::cout << "Guessed letters: ";
    for (char c : guessedLetters) {
        std::cout << c << " ";
    }
    std::cout << std::endl;
    std::cout << "Mistakes made: " << mistakesMade << std::endl;
}

int main() {
    std::string secretWord = "computer";
    std::vector<char> guessedLetters;
    int mistakesMade = 0;
    bool gameOver = false;

    while (!gameOver) {
        displayBoard(secretWord, guessedLetters, mistakesMade);
        char guess;
        std::cout << "Enter your guess: ";
        std::cin >> guess;

        if (std::find(guessedLetters.begin(), guessedLetters.end(), guess) != guessedLetters.end()) {
            std::cout << "You have already guessed that letter!" << std::endl;
        } else {
            guessedLetters.push_back(guess);

            if (std::find(secretWord.begin(), secretWord.end(), guess) == secretWord.end()) {
                mistakesMade++;
                if (mistakesMade == 6) {
                    std::cout << "Game over! The secret word was: " << secretWord << std::endl;
                    gameOver = true;
                }
            } else {
                bool foundAllLetters = true;
                for (char c : secretWord) {
                    if (std::find(guessedLetters.begin(), guessedLetters.end(), c) == guessedLetters.end()) {
                        foundAllLetters = false;
                        break;
                    }
                }
                if (foundAllLetters) {
                    std::cout << "Congratulations! You guessed the secret word: " << secretWord << std::endl;
                    gameOver = true;
                }
            }
        }
    }

    return 0;
}
