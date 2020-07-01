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
To add elements to this query field we use the **textContent** where we can set up a value to add String values 
to the Query Selectors.
```javascript
const render = () => {
    puzzleEl.innerHTML = '' // We set the Puzzle element to be completely empty 
    guessesEl.textContent = game1.statusMessage // Status of game - playing, won , game over

    game1.puzzle.split('').forEach((letter) =>{ // spiliting the puzzle words into different sets of words
        const letterEl = document.createElement('span')
        letterEl.textContent = letter
        puzzleEl.appendChild(letterEl)
    }) 
}


```

### Adding an Event Listener on the web browser
The **EventTarget** method *addEventListener()* sets up a function that will be called whenevver the specified event is delivered to the target.

```javascript
window.addEventListener('keypress', (e) => { // there are multiple instances of the eventListener not just keypress 
    const guess = String.fromCharCode(e.charCode)
    game1.makeGuess(guess)
    render()
})
```
On the eventListener we give a second argument **e** this takes the instance of the eventListener we can use this to get the value from the EventListener function. In the code above the const variable **guess** takes the value from the EventListener and this is passed on to the *makeGuess()* function.

