# Anki-Cousins
Bury non-sibling similar cards

# This add-on is based on (mostly copied from) anki cousins by AlexRiina
#### The only changes i made are minor changes in interface and a change in siliraity test to maximize accuracy.
[Original add-on page (anki website)](https://ankiweb.net/shared/info/1072815885)
[Original add-on github page](https://github.com/AlexRiina/anki_cousins)

#### Some questions you might have about this add-on:

* what does it do?
> it searches for similar cards in the deck you're reviewing and if two or more cards are similar it'll bury them (except for one you reviewed) till next day. it basically does what **Bury Related Cards** Does but with non-sibling cards
* What's the difference betweem this and the original one?
> I have changes 4 things in thid add-on:
> 1. Added "Bury COusin Options" to Tools menu, for quick access
> 2. Added some tooltips so you know what to do with each option, tooltips are minimal and if you haven't read the manual already, you might not find them useful.
> 3. Changed some minor things in Original UI (not that importatnt)
> 4. Which i think is the most important one. i have tweaked sililarity test a bit so it'll detect all clozes and basics regardless of what you might have entered after :: in cloze hint. (made it case insensitive too)
> here are eacmples of how it's changes:
> * in original one similarity between **"this is a basic test"** and **"THIS IS A BASIC TEST"** is 20% though they're identical. but in this version the similarity is 100%
> * in original one similarity between **"this is a cloze test"** and **"this is a {{c1::cloze}} {{c2::test}}"** is around 70% which might not be a serious problem to a lot of peple (but theire identical anyways) the problem that this might cause is in the next example. (similarity between those two is 100% in this version)
> * in original one similarity between **"this is a cloze test"** and **"this is a {{c1::cloze::something something to decrease similarity}} {{c2::test::this is some more thing just for the same thing}}"** is around 25% but they're 100% similar in this version
> HOWEVER, I DON'T I DON'T CLAIM CREDIT FOR ANY PART OF THIS CODE, AND IT'S ALL AlexRiina's CODE NAD ALL CREDIT GOES TO HIM
* How to set it?
> go to Tools -> Bury Cousin Options and click on Add Rule button.
> in "On Note" and "To Note" options you'll have to select note types you want the add-on to compare.
> in "Match Field" part you'll have to write down the field name you want to compare.
> in "Matcher" you can choose what kind of test you want to run on those fields.
* What's the difference between different tests?
> to answer that question you'll have to understand how each option works. so i'm gonna explain taht to you (as simple as i can)
> * Prefix test: it supposedly compares the first part the sentence till it gets to value that's not the same for both fields.
> for example: you have "this is a test" and "this is NOT a test" as you fields. what this test does is it asigns number to each letter of both fields (0: t | 1: h | 2: i). it does this to the point that the character is not the same for both of these fields (in this case, N in "not"). then it gets the final number and ads 1 to it. if this case, final number will be 11, which is number of character till before N in "NOT". (Call this number "Match percent")
> that was the first par, then it gets the field that has most characters and mutiplis it by the similarity precent you have set in add rule. in this case second sentcent has more characters (18 characters) and if you have set similarity percent on 0.8, the final number will be 14.4 (Call this "Similarity percent")
> then add-on compares "match Percent" amd "Similarity percent" and if "Match Pecent" > "similarity Percent" it count these two cards as cousins.
> * By Similarity: this compares the whole sentence, and i think is the most accurate and usefull test (i just use this one that's why i improved it to maximize it's accuracy)
> it uses a built-in python function function and uses it's algorithm to compare the sentences.
> I, myself don't rally know how this algorithm works. but if you're interested in knowing how it works, search for "python SequenceMatcher"
> using this method to compare "xxyy" and "xyxy" will return 75% match and comparing "xxyy" and "xyxyy" will return 89% match
> * Contains: checks if the first field (field name in front of "On Note") contains the seconf field (field name in front of "To Note") similarity has no functionality in this method and using this method will only return True if fierst field contains second field.
> for example if you have "this is a test and something" on first field and "this is a test", using this test will return True because firs field containd second field ("this is a test")
> * Contained By: Checks if first field is contained by second field. it's basically the previous method.
> for example, if you have "this is a test" on the first field and "this is a test and something" this test will return True, because seconf field contains firsr field.
> * Cloze Answers Contained By: checks if cloze answer ({{c1::__Cloze Answer__}}) in contained by any other card.
> for example if you have "this is a __Cloze Answer__ test" on first field and on second field you have "this is my {{c1::__Cloze Answer__}} test" it'll return True
* Cards buried by this add-on are counted as automatically buried or manually buried cards?
> as this add-on uses the same function as bury sibling function uses in anki source code, cards that this add-on buries are counted as automatically buried cards and when you want to unbury them you'll have to click "Buried siblings" when anki asks you whether you want to unbury manually buried cards or buried siblings.

* I have also added an adding tag to cousin notes, however i have comented out the parts that do that. (thought you might not like that)
if you like to enable than option, remove "#" in front of lines 61 to 82 in main.py file


**if you have too many cards on a deck (more than 1000) using this add-on to bury cousins might make your anki laggy (just a little bit though, not a big deal)**
