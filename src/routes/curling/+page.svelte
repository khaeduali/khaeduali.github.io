<script>
import {
    onMount
} from "svelte";

let timer = 0
let stone = {
    x: 0,
    y: 0,
    angle: 0,
    speed: 1,
    acceleration: 0.99
}
let sweepTimer = 0
let currentMode = "angle" // "speed", "sweep"

onMount(() => {
    setInterval(() => update(), 10)
})

function reset() {
    sweepTimer = 0
    stone = {
        x: 0,
        y: 0,
        angle: 0,
        speed: 1,
        acceleration: 0.99
    }
    currentMode = "angle"
}

function update() {
    timer++
    switch (currentMode) {
        case "angle":
            stone.angle = Math.sin(timer * 0.05) * 0.25
            document.getElementById("target").style.rotate = stone.angle + "rad"
            break

        case "speed":
            stone.speed = (1 + Math.sin(timer * 0.05) * 0.5)
            document.getElementById("target").style.transform = "scaleX(" + stone.speed + ")"
            break

        case "sweep":
            document.getElementById("target").style.opacity = 0

            if (--sweepTimer < 0) {
                stone.acceleration -= 0.00005
                stone.speed *= stone.acceleration
            }

            for (let i = 0; i < 8; i++) {
                if (stone.x < 1120)
                    stone.x += stone.speed * Math.cos(stone.angle)
                stone.y += stone.speed * Math.sin(stone.angle)
            }

            console.log(stone.x)
            document.getElementById("stone").style.marginLeft = stone.x + "px"
            document.getElementById("stone").style.marginTop = stone.y + "px"
            if (document.getElementById("internal").style.opacity > 0)
                document.getElementById("internal").style.opacity -= 0.1
            break
    }
}

function handleKeyEvents(event) {
    if (event.keyCode != 32)
        return
    switch (currentMode) {
        case "angle":
            currentMode = "speed"
            break

        case "speed":
            currentMode = "sweep"
            break

        case "sweep":
            if (sweepTimer < -10) {
                sweepTimer = 10
                document.getElementById("internal").style.opacity = 1
            }
            break
    }
}
</script>

<svelte:window on:keydown={handleKeyEvents} />

<main>
    <div class="goal"></div>
    <div class="goal" id="goal2"></div>
    <div class="goal" id="goal3"></div>

    <div id="target"></div>

    <div id="stone">
        <div id="internal"></div>
    </div>
</main>

<style>
main {
    border: solid 5px #b4befe;
    border-radius: 10px;
    width: 75%;
    height: 40%;
    min-height: 600px;
    background-color: #1e1e2e;
    margin: auto;
    left: 12.5%;
    margin-top: 7%;
    margin-bottom: 5%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;
    position: absolute;
}

.goal {
    width: 150px;
    height: 150px;
    left: calc(75% - 37.5px);
    border: solid 5px #b4befe;
    border-radius: 50%;
    position: fixed;
    box-shadow: 0px 0px 30px #b4befe inset, 0px 0px 4px #b4befeaa;
}

#goal2 {
    width: 75px;
    height: 75px;
    left: 75%;
}
#goal3 {
    width: 225px;
    height: 225px;
    left: calc(75% - 75px);
}

#target {
    width: 200px;
    height: 10px;
    border: dashed 2px #b4befe;
    border-radius: 4px;
    box-shadow: 0px 0px 4px #b4befe inset, 0px 0px 4px #b4befe;
    transform-origin: left;
    opacity: 1;
}

#internal {
    top: inherit;
    left: inherit;
    border: inherit;
    border-radius: inherit;
    box-shadow: inherit;
    position: inherit;
    scale: 2;
    opacity: 0;
}

#stone {
    width: 10px;
    height: 10px;
    border: solid 5px #b4befe;
    border-radius: 50%;
    box-shadow: 0px 0px 4px #b4befe inset, 0px 0px 4px #b4befe;
    position: fixed;
}
</style>
