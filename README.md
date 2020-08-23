# shakespeare
Python code that parses html files of Shakespeare's plays and converts them to a JSON file.

After searching online for an API to interact with Shakespeare's plays and finding only one from the Folger Shakespeare Library (https://www.folgerdigitaltexts.org/api) and finding it lacking for what I needed, I chose to build a Python script that would convert Shakespeare's plays from MIT (http://shakespeare.mit.edu/) into an easy to use Python Dictionary and, relatedly, as JSON. The ultimately goal, and purpose for building and converting the play texts, is to build a Shakespeare Trivia Game.

The Python script is straightforward and may well provide opportunities for optimization, but, hey, it works!

There are four Python functions: (1) format_play, (2) classifier, (3) extractor, and (4) roman_numeral_to_integer. I tried to compartmentalize into functions the logic that is repeated, which is a simple rule I try to follow when writing any code: do not repeat yourself.

The format_play function is the main function that serves to build and populate a Python dictionary and then convert to JSON the Shakespeare play. I download and save locally the HTML file for a play from MIT. Read in the file and then with a 'for' loop, iterate, line by line, through the play doing the following: (1) classify the line, (2) extract the data from the HTML tags, (3) add the line to the Python dictionary, and (4) keep track of the play structure (scenes, speeches, dialogue lines, etc.) to assist creating the Python dictionary. This function ultimately returns the Python dictionary.

The classifier function takes the line from format_play and based on unique characteristics classifies it as (1) title, (2) 
