# English-Dictionay
English Dictionay to help find meaning of words setup in Python

#English Threasus

import json #library
from difflib import get_close_matches

data = json.load(open("data.json"))

def meaning(w):
    word = w.lower()

    if word in data:
        return(data[word])
    elif word.title() in data:
        return(data[word.title()])
    elif word.upper() in data:
        return(data[word.upper()])
    elif len(get_close_matches(word,data.keys())) > 0:
        ans = input("Did you mean %s instead? Enter Y if yes, or N for no: " %get_close_matches(word,data.keys())[0])
        if ans == "Y":
            return(meaning(get_close_matches(word,data.keys())[0]))
        elif ans =="N":
            return("The word doesnot exit . Please double check it.")
        else:
            return("We didn't understand your entry.")
    else:
        return "The word doesnot exit . Please double check it."

word = input("Enter a word: ")

output = meaning(word)

if isinstance(output,list):
    for item in output:
        print(item)
else:
    print(output)


