# AnkiFlashcardGenerator
Generate Flashcards via Online Dictionaries
Anki Flashcards Automation - Minimum Viable Product (MVP)

Overview

This repository contains Python code designed to automate the creation of Anki flashcards. The primary purpose of this script is to fetch word definitions and conjugations from an online source and add them to an Anki deck.

Currently, the code:

Uses Selenium to navigate to a Tagalog word dictionary.
Extracts the word’s information such as the part of speech, conjugations, and definitions.
Automates the process of adding this information to Anki using the AnkiConnect API.
This code is a Minimum Viable Product (MVP), serving as a foundation for future development. While it performs the basic tasks required to generate flashcards, there are known limitations and areas for improvement. Over the coming months, this project will be refined to improve robustness, handle edge cases, and enhance usability.

Prerequisites

1. Software
Python 3.11+
Anki with AnkiConnect plugin (AnkiConnect allows external tools to interact with Anki via an API)
Google Chrome and ChromeDriver (for Selenium)
Selenium for web scraping
BeautifulSoup for HTML parsing
2. Python Libraries
Install the required libraries using pip:

bash
Copy code
pip install selenium webdriver-manager requests beautifulsoup4 unidecode
3. AnkiConnect Setup
Ensure that the AnkiConnect plugin is installed and running on Anki. AnkiConnect enables the communication between your Python script and Anki's API.

Features

Deck Creation: Automatically create a new deck in Anki using invoke('createDeck').
Flashcard Addition: Add words along with their definitions, roots, and conjugations to the appropriate Anki deck.
Duplicate Detection: The script checks if a card already exists in the deck to avoid duplicates.
Word Scraping: Use web scraping to fetch relevant word data from a Tagalog dictionary.
Usage

Run the Script: To generate flashcards, run the Python script. It will interact with Anki and a web dictionary to create flashcards based on a predefined list of words.
Check for Existing Cards: The script first checks if the word already exists in the Anki deck to avoid duplication.
Flashcard Generation: If the word doesn’t exist in the deck, the script scrapes the definition, root, and conjugation information and formats it for a flashcard.
Add to Deck: The new flashcard is automatically added to the specified Anki deck.
Example Code Usage

python
Copy code
words_to_add = ['lakaran','asahan','basahan']

for word in words_to_add:
    if check_if_word_exists(word):
        print(f"{word} is already in the deck!")
        continue
    url = find_correct_word(word, 'verb')
    front, back = create_front_and_back(url, word)
    new_card_data = {'Front': front, 'Back': back}
    
    add_note_params = {
        'note': {
            'deckName': 'test1',  # The deck name
            'modelName': 'Basic',  # Anki note model
            'fields': new_card_data
        }
    }
    
    invoke('addNote', **add_note_params)
Known Issues & Future Enhancements

Current Limitations
Error Handling: Some edge cases for error handling (e.g., missing conjugations) need improvement.
Scraping Reliability: Occasionally, web scraping might fail due to changes in the dictionary website.
Duplicate Flashcards: The code checks for duplicates but may miss some edge cases.
Planned Enhancements
Improved Parsing: Enhance HTML parsing to better handle different word types and improve accuracy.
Optimization: Optimize the Selenium-based scraping to reduce load times and improve performance.
Refinement in Conjugation Handling: Add more sophisticated handling for verbs and conjugation tenses.
Advanced Error Handling: Improve error detection and handling for better script reliability.
Over the next few months, this code will be continuously refined and enhanced to improve functionality, efficiency, and flexibility. Stay tuned for updates!
