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

## Requests.js

### Fetching the puzzle word from the API
To fetch random puzzle words we derive it by fetching randoms from an API service. The function **startGame()** will be aync function which uses the **await** method that waits for the API to sent a response to the Hangman application. 
```javascript
const startGame = async () => {
    const puzzle = await getPuzzle('2')
    game1 = new Hangman(puzzle, 5)
    render()
}
```
#### Method to check if the response from the server is correct or wrong
Remember the status response code should always be 200 or else there might be some errors when the response is recevied from the server.

```javascript
const getPuzzle = async (wordCount) => {
   const response = await fetch(`http://puzzle.mead.io/puzzle?wordCount=${wordCount}`)
   
   if (response.status === 200) {
       const data = await response.json()
       return data.puzzle
   } else {
       throw new Error('Unable to get puzzle')
   }
}
```

### Combing two API Method calls 
The following code shows how to use the combination of two API method calls. The API method is the **getCurrentCountry** async function which calls the *getLocation()* to fetch the country code depending on the IP address (It is an API). The return statement from the **getCurrentCountry**  will be pushed into calling the the **second API method** 

```javascript 
const getCurrentCountry = async () => {
   const location = await getLocation()
   return getCountry(location.country) // this line calls the second API Method 
}

const getCountry = async (countryCode) => {
   const response = await fetch('http://restcountries.eu/rest/v2/all')

   if (response.status === 200) {
       const data = await response.json()
       return data.find((country) => country.alpha2Code === countryCode)
   } else {
       throw new Error('Unable to fetch the country')
   }
}

const getLocation = async () => {
   const response = await fetch('http://ipinfo.io/json?token=1a11bd55cc8f9c')

   if (response.status === 200) {
       return response.json()
   } else {
       throw new Error('Unable to get the current location')
   }
}


```
  


