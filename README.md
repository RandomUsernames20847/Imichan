# Imichan - crappy jp popup dict

## Development Journal
Ok so first of all what does this project need...
Right. An analysis for my teacher to read. It'll be pretty boring.

> What problem are you solving?
> Japanese students cannot read or understand Japanese text quickly. They have to copy-paste it into a translator or, if it's in an image, pull out their phones if they're available to use the handwriting feature on Google Translate Mobile. If they're a student who can't have phones, bad luck. Even if they do have a phone, they have to do this for every single kanji they can't read in the passage they are looking at. The Chrome Webstore extensions rikai-kun and yomi-chan solve this problem, but only within Chromium web browsers and they cannot read from images.
> 
> 意味ちゃん (imi-chan) hopes to be a desktop app running in the background that can show the definitions and pronunciations of any hovered-over word or kanji. Even if it's from an image. This would be very useful for apps like Word and OneNote for Japanese students, or if a pdf or image with Japanese text is sent. An integration with the Anki flash-card app can turn this into a learning tool for non-Japanese students.
>
> How is it unique?
To my knowledge, there is NO other app that has capabilities like this because it is such a small niche. My experience in using other desktop programs like KanjiTomo and JGlossator have been difficult, clunky, limited (showing Kanji information only, not the definition of the whole word) and resource-intensive. I believe I can optimise an app enough to extract text cleanly but still provide a feature-rich program.

Ok so now.. uh.. 
## What should it be able to do?
- Extract text from the app the cursor sees at that location
- Display deinitions, pronunciation, modifications applied to the selected word when required according to multiple dictionary search results
- Display kanji information when required (stroke order, kun/on reading)
- Extract text from any image the cursor sees, even if it is rotated
- Customisable keybinds
+ Customisable popup appearance
+ Send words or kanji and their definitions to Anki as a new flash card
### Include all kanji info Rikaikun carries:
- Unicode
- PinYin
- Every. Single. Kanji Reading.
- Skip Pattern (Identification)
### Include all word information Yomichan carries:
> - JMDict Dictionary
> + JMneDict Name Dictionary
> + KireiCake Slang Dictionary
> - KanjiDic Kanji Dictionary
> + KanjiUM Pitch Accents

Okok that's a lot of requirements... Uhh
Let's journal out progress and make a plan!
First phase: Creating a function to exact search a word from the main definitions dictionary (JMDict) and get its definitions
1. Download JMDict
2. Read the json and search for the word
3. Get the definition
4. Display it
Easy! I got this. This should be finishable in 2 weeks.

## Day 2

... Not easy.
Issues I've encountered:
- This is a version of JMDict (originally in very crappy EPWING format) that is converted to JSON and has no documentation.
- There are multiple (34) JSON files.
- I spent half a day trying to download Json.NET, which I don't know how to use.
- There are multiple entries for the same word for different definitions and **WHY ARE THERE DUPLICATES OF DEFINITIONS**

Ok so let's try to handle the first issue. Gotta understand the dictionary first.
It's an array [] of definitions, and each entry looks like this: (1st definition in term_bank_32.json)
```json
["取扱店","とりあつかいてん","n","",2,["service point","agency","office"],2837181,""]
```
Let's linesplit that for readability, and compare it to yomi-chan results and a *very* similar word to understand what's going on.

Word 1:
```json
[ "取扱店",  // Big text to be displayed, usually kanji
  "とりあつかいてん",  // Hiragana if the word isn't already in hiragana/katakana
  "n",  // Tags for the word separated by spaces; "n" means "common noun"
  "",  // ???
  2,  // Definition ID: Words that have multiple definition entries will have one of these
  ["service point","agency","office"],  // Definition
  2837181,  // Word ID: Words that are the same just written in different ways will have the same Word ID
  ""  // ???
]
```

Other definition entry of this word: (they are the same!)
```json
["取り扱い店","とりあつかいてん","n","",3,["store dealing in a particular item","distributor"],2837181,""]
```
