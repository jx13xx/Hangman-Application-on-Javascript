# Hangman Application on Javascript
 Hangman App completely built on Javascript 
 
 <img src="images/cover.jpg">
 
 
The general syntax of the Index.html file contains the following Javascript files 

- Requests.js
- Hangman.js
- App.js



## App.js
The *app.js* file contains all the event listeners, querySelectors(text fields and labels)
It also uses the function render() to render the puzzle on the webpage 

### Creating the Query Selectors and Function return callback 
```javascript
const puzzleEl = document.querySelector('#puzzle') // documentSelector for puzzles i.e A_B__D_E
const guessesEl = document.querySelector('#guesses') //documentSelector for guesses made


```
