# shakespeare
Python code that parses html files of Shakespeare's plays and converts them to a JSON file.

After searching online for an API to interact with Shakespeare's plays and finding only one from the Folger Shakespeare Library (https://www.folgerdigitaltexts.org/api) and finding it lacking for what I needed, I chose to build a Python script that would convert Shakespeare's plays from MIT (http://shakespeare.mit.edu/) into an easy to use Python Dictionary and, relatedly, as JSON. The ultimately goal, and purpose for building and converting the play texts, is to build a Shakespeare Trivia Game.

The Python script is straightforward and may well provide opportunities for optimization, but, hey, it works!

There are four Python functions: (1) format_play, (2) classifier, (3) extractor, and (4) roman_numeral_to_integer. I tried to compartmentalize into functions the logic that is repeated, which is a simple rule I try to follow when writing any code: do not repeat yourself.

The format_play function is the main function that serves to build and populate a Python dictionary and then convert to JSON the Shakespeare play. I download and save locally the HTML file for a play from MIT. Read in the file and then with a 'for' loop, iterate, line by line, through the play doing the following: (1) classify the line, (2) extract the data from the HTML tags, (3) add the line to the Python dictionary, and (4) keep track of the play structure (scenes, speeches, dialogue lines, etc.) to assist creating the Python dictionary. This function ultimately returns the Python dictionary.

The classifier function takes the line from format_play and based on unique characteristics classifies it as (1) title, (2) act, (3) scene, (4) direction, (5) speech, and (6) dialogue. Based on tell-tale signs of each of these types, the classifer function analyzes the line and returns a category value.

The extractor function takes the line type and line from format_play and based on the line type, it performs string manipulation to extract the "meat" of the line or the relevant portions and discard the HTML tags. This function then returns the relevant portion to format_play.

Finally, the roman_numeral_to_integer function takes the line type and line from format_play and translates the roman numeral from the play text into an iteger and returns that integer. This is important for creating the dictionary keys. For example, the HTML text will say "ACT IV", but the Python dictionary will use act4.

The Python dictionary structure for a play is laid out below:
{"title": [play_title], 
 "text": {
          "act1: {
                   "title": [act_title], 
                   "scene1": {
                              "title": [scene_title],
                              "description": [scene_description],
                              "content": {
                                          "direction1: [direction_description],
                                          "speech1": {
                                                      "speaker": [speaker_name],
                                                      "dialogue": {
                                                                   "line1.1.1": [dialogue_text],
                                                                   "line1.1.2": [dialogue_text]
                                                                   }
                                                      },
                                          "speech2": {
                                                      "speaker": [speaker_name],
                                                      "dialogue": {
                                                                   "line1.1.3": [dialogue_text],
                                                                   "line1.1.4": [dialogue_text]
                                                                   }
                                                      }
                                           }
                               }
                    }
          }
}

- Every play will have a "title" key with a string value. Example: "title": "The Tragedy of Hamlet, Prince of Denmark".
- Every play will have a "text" key with a dictionary value that serves as the container for the play's content.
- Every play will have 1 or more acts with keys that are a string of 'act' followed by the act number and a value of a dictionary. The dictionary will have a "title" key with a value equal to the language directly from the play, such as "ACT I". Example: "act1".
- Every play will have 1 or more scenes with keys that are a string of 'scene' followed by the scene number and a value of a dictionary. The dictionary will have a "title" key with a value equal to the language directly from the play, such as "SCENE I", a "description" key with a value equal to the language direclty from the play, such as "Elsinore. A platform before the castle.", and a "content" key with a value equal to a dictionary. Example: 'scene1'. The "content" dictionary may include any number of stage directions with a key that is a string 'direction' followed by the direction number (this iterates using a counter and resets to one for each scene). It will also include one or more speeches, which is a container for a speaker and all their subsequent consecutive speaking lines. A speech has a key equal to the string 'speech' followed by the speech number (this iterates using a counter and resets to one for each scene). The speech key has a dictionary value that includes a 'speaker' key and value equal to a string that identifies the speaker, such as '"BERNARDO", and a "dialogue" key with a dictionary value that includes 1 or more dialogue lines. The diaglogue lines use a key of 'line' followed by a unique ID, such as "line1.1.1", which represents the act.scene.line_number, and a value equal to the dialogue text, such as ""Who's there?". The unique ID for each line will iterate in the line position (third position) and reset to one at the start of each new scene.
