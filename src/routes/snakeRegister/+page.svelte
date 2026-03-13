<script>
import {
    onMount
} from "svelte";

let pass = $state("")
let hovering = $state(false)

let playerPosition = $state(0)
let letter = $state({
    x: -20,
    y: 0,
    letter: 'x'
})
let moveDirection = 1.5
const charSet = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0, 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];

function handleSubmit() {
    hovering = false;
    pass = ""
    playerPosition = 0
    moveDirection = 1.5
    resetLetter()
}

onMount(() => {
    resetLetter()

    setInterval(() => update(), 10)
})

function resetLetter() {
    letter.y = -20
    letter.x = 10 + Math.round(Math.random() * 400)
    letter.letter = charSet[Math.round(Math.random() * (charSet.length - 1))]
}

function changeDirection(event) {
    if (event.keyCode == 8 && pass.length > 0)
        pass = pass.slice(0, -1)

    if (event.keyCode == 37)
        moveDirection = -1.5
    else if (event.keyCode == 39)
        moveDirection = 1.5
}

function update() {
    if (!hovering)
        return;

    if (moveDirection < 0 && playerPosition - 1 > 0)
        playerPosition += moveDirection

    if (moveDirection > 0 && playerPosition + 1 < 420)
        playerPosition += moveDirection

    document.getElementById("player").style.left = (playerPosition) + "px";

    letter.y++
    if (letter.y > 169) 
        resetLetter()

    if (letter.y > 150 && letter.x < playerPosition + 15 && letter.x > playerPosition - 15)
    {
        pass = pass.concat(letter.letter)
        resetLetter()
    }

    document.getElementById("char").style.left = (letter.x) + "px";
    document.getElementById("char").style.top = (letter.y) + "px";
}
</script>

<svelte:window on:keydown={changeDirection} />

<main>
    <div class="container_offshoot" style="margin-top:-52vh; left: -1%;">
        <h1>Skapa ett lösenord</h1>
    </div>
    <form class="formulär" on:submit|preventDefault={handleSubmit}>
        <input type="text" id="pass"  bind:value={pass} on:focusin={hovering=true} readonly>
        <div class="snake_field" class:visible={hovering}>
            <p id="char">[{letter.letter}]</p>
            <p id="player">^</p>
        </div>
        <p></p>
        <input id="submitbutton" type="submit" value="Registrera" style="font-family: courier;">
    </form>
</main>

<style>
main {
    border: solid 5px #b4befe;
    border-radius: 10px;
    width: 35%;
    min-width: 370px;
    height: 40%;
    min-height: 260px;
    background-color: #1e1e2e;
    margin: auto;
    left: 30%;
    margin-top: 10%;
    margin-bottom: 5%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;
    position: absolute;
}

.container_offshoot {
    border: solid 5px #b4befe;
    border-radius: 10px;
    height: 5%;
    width: 100%;
    min-height: 70px;
    background-color: #1e1e2e;
    margin: auto;
    margin-top: 65vh;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;
    position: absolute;
}

#player {
    position: fixed;
    top: 82%;
    left: 0px;
    font-weight: bolder;
}

#char {
    position: fixed;
    font-weight: bolder;
}

.formulär {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;

    width: auto;
    height: auto;

    color: #b4befe;
    font-family: courier;
    text-align: center;
    z-index: 2;
}

input,
.snake_field {
    background-color: #181825;
    color: #b4befe;
    border-color: #b4befe;
    border-style: solid;

    width: 80%;
    max-width: 420;
    min-width: 420;
    margin-left: auto;
    margin-right: auto;
    border-radius: 16px;
    z-index: 2;
    scale: 1;
    transition: scale 0.2s;
}

input {
    padding: 10px;
}

.snake_field {
    opacity: 0;
    margin-top: 0px;
    min-height: 0px;
    max-height: 0px;
    transition: all 0.2s;
}

.snake_field.visible {
    opacity: 1;
    margin-top: 20px;
    min-height: 200px;
    max-height: 200px;
}

input:hover {
    scale: 1.1;
}

#submitbutton {
    margin-top: 2%;
    font-size: 1em;
    height: 40px;
    font-weight: bolder;
    background-color: #b4befe;
    border-color: #181825;
    color: #181825;
    border-style: solid;
}

h1 {
    font-family: 'Courier New', Courier, monospace;
    color: #b4befe;
    margin-left: auto;
    margin-right: auto;
}
</style>
