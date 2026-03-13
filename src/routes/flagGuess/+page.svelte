<script>
	import { onMount } from "svelte";

 // https://api-ninjas.com/api/countryflag
let guess = $state("")
let guessAmt = $state(0)
let guessedCorrectly = $state(0)
let accuracy = $state(0)

let lastFlag = $state("None")
let lastGuess = $state("None")

let flagDB

let flagIndex = -1
let flagLink = $state("")

function initFlag() {
    flagIndex = Math.floor(Math.random() * flagDB.length)

    flagLink = "https://flagcdn.com/h120/" + flagDB[flagIndex].code.toLowerCase() + ".png"
}

onMount(async () => {
    flagDB = await getFlags()

    console.log(flagDB)
    initFlag()
})

async function getFlags() {
    const db = await fetch("https://cdn.simplelocalize.io/public/v1/countries")
    const json = await db.json()

    if (db.ok) 
        return json
    else throw new error("Something went wrong!")
}

function handleSubmit() {
    if (guess.length < 2)
        return;

    guessAmt++

    if (guess.toLowerCase() === flagDB[flagIndex].name.toLowerCase())
        guessedCorrectly++

    if (guessedCorrectly > 0 && guessAmt > 0)
        accuracy = Math.floor(guessedCorrectly / guessAmt * 100) 

    lastFlag = flagDB[flagIndex].name
    lastGuess = guess
    guess = ""
    initFlag()
}
</script>

<main>
    <div class="bg" style="background-color: #181825"></div>  
    <div class="bg2 bg"></div>  

    <div class="flag_container">
        <p>{accuracy}% ({guessedCorrectly}/{guessAmt})</p>
        <p>Last flag: {lastFlag}</p>
        <p>You guessed: {lastGuess}</p>
        <img src={flagLink}>
    </div>

    <form class="formulär" on:submit|preventDefault={handleSubmit}>
        <input placeholder="Guess the flag..." bind:value={guess}>
        <input type="submit" value="Guess">
    </form>

</main>

<style>
.bg {
    display: inline;
    top: 0;
    left: 0;
    background-size: cover;
    position: fixed;
    z-index: -9;
    width: 100%;
    height: 100%;
}
.bg2 {
    background-image: url("https://raw.githubusercontent.com/orangci/walls-catppuccin-mocha/master/dark-waves.jpg");
    filter: blur(15px) hue-rotate(130deg) saturate(200%);  
    opacity: 0.25;
    z-index: -8;
}

.flag_container {
    width: 340px;
    height: 240px;
    margin: auto;
    margin-top: 5%;
    margin-bottom: 10%;
}

.formulär {
    width: 100%;
    height: 80px;
    margin: auto;
    display: flex;
    flex-direction: column;
}

img {
    width: 340px;
    height: 240px;
    margin: auto;

    border: #fab387 4px solid;
    box-shadow: 0px 0px 10px 5px #fe640b33;
    border-radius: 16px;
}

input {
    width: 256px;
    font-family: courier;
    font-weight: bold;
    padding: 10px;
    margin: auto;

    background-color: #181825;
    color: #fab387;

    border: #fab387 4px solid;
    box-shadow: 0px 0px 10px 5px #fe640b33;
    border-radius: 16px;
    
    margin-top: 20px;
}

p {
    color: #fab387;
    font-family: courier;
    font-weight: bold;
    text-shadow: 0px 0px 5px #fe640b33;
}
</style>

