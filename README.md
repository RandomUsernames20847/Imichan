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
# Include all kanji info Rikaikun carries:
- Unicode
- PinYin
- Every. Single. Kanji Reading.
- Skip Pattern (Identification)
# Include all word information Yomichan carries:
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
3. Get the diction
