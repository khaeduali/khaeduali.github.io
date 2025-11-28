<script>
import { fade } from 'svelte/transition'
let varor = $state([]);

let addedElement = $state("");

function handleSubmit() {
    if (typeof(addedElement) === typeof("  ") && addedElement.length > 0) {
        if (addedElement.length > 28) {
            alert("Max antal bokstäver är 28!")
            addedElement = ""
            return
        }
        varor.push({name: addedElement, köpt: false, priority: 0})
        addedElement = ""
    }
}
</script>

<main>
    <div class="container">
        <h1>-Shoppinglista-</h1>
        <div class="categories_container">
            <section>
                <h2>--Att köpa--</h2>
                <ol>
                    {#each varor as vara}
                    {#if !vara.köpt}
                    <button type="button" on:click={() => vara.köpt = true}>˅</button>
                    <div transition:fade>
                    <input type="number" id="prio" bind:value={vara.priority} on:click={()=>varor.sort((a, b) => b.priority-a.priority)}>
                    <li  on:click={() => varor.splice(varor.indexOf(vara), 1)}>
                        {vara.name}
                    </li>
                    <div class="underline"></div>
                    </div>
                    {/if}
                    {/each}
                </ol>
                
        <form class="formulär" on:submit|preventDefault={handleSubmit}>
                <input type="text" id="items"  bind:value={addedElement}>
                <input id="submitbutton" type="submit" value="Lägg till">
        </form>
            </section>

            <section>
                <h2>--Köpt--</h2>
                <ul>
                    {#each varor as vara}
                    {#if vara.köpt}
                    <div transition:fade>
                    <li  on:click={() => varor.splice(varor.indexOf(vara), 1)}>
                        {vara.name}
                    </li>
                    <div class="underline"></div></div>
                    {/if}
                    {/each}
                </ul>
            </section>
        </div>
    </div>
</main>

<style>
.container {
    background-color: #11111b;
    width: 60vw;
    max-width: 500px;
    height: fit-content;
    border-radius: 20px;
    border: 2px solid #74c7ec;
    margin: auto;
    margin-top: 10vh;

    display: grid;
    grid-template-rows: 1fr 9fr 1fr;
}

.categories_container {
    height: 100%;
    background-color: #181825;
    display: grid;
    grid: repeat(2, 1fr);
    grid-gap: 20px;
    padding: 20px;
}

.categories_container section {
    position: relative;
}

.categories_container section:nth-child(even) {
    border: 2px solid #cba6f7;
}

.categories_container section:nth-child(odd) {
    border: 2px solid #b4befe;
}

.categories_container section:nth-child(even) h2 {
    color: #cba6f7;
}

.categories_container section:nth-child(odd) h2 {
    color: #b4befe;
}

.categories_container section:nth-child(even) li {
    color: #cba6f7;
}

.categories_container section:nth-child(odd) li {
    color: #b4befe;
}

.categories_container section:nth-child(even) input {
    border-color: #cba6f7;
    color: #cba6f7;
}

.categories_container section:nth-child(odd) input {
    border-color: #b4befe;
    color: #b4befe;
}

.categories_container section:nth-child(even) .underline {
    background-color: #cba6f7;
}

.categories_container section:nth-child(odd) .underline {
    background-color: #b4befe;
}

form {
    height: fit-content;
    position: absolute;
    bottom: 10px;
    left: 18%;
}

input {
    font-family: courier;

    background-color: #181825;
    border-style: solid;

    width: 40%;

    display: inline;
    margin: auto;
    margin-left: 20px;
    margin-top: 10px;
    text-align: center;
    border-radius: 16px;
    z-index: 2;
    scale: 1;
    transition: scale 0.2s;
}


input:hover{
    scale: 1.1;
}

#prio {
    color-scheme: dark;
    width: 10%;
    margin-top: 0;
    left: 70%;
    position: absolute;
}


ul,
ol {
    margin-left: 20px;
}

section {
    background-color: #11111b;
    width: 100%;
    height: 100%;
    border-radius: 20px
}

h1 {
    color: #74c7ec;
    width: auto;
    margin: auto;
}

li {
    width: fit-content;
    font-family: courier;
    text-decoration: none;
    transition: all 0.3s;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
}

li:hover{
    margin-left: 10px;
  	text-shadow: 0px 0px 4px  #ff0000;
    text-decoration: line-through;
    cursor: pointer;
}

button {
    margin-left: 75%;
    display:inline;
    width: auto;
    height: auto;
    position: absolute;
    background-color: transparent;
    border-color: #b4befe;
    color: #b4befe;
    border-style: solid;
    border-radius: 8px;  
    scale: 0.85;
    transition: all 0.2s;
    font-weight: bolder;
}

button:hover {
    scale: 1;
}

.underline {
    height: 2px;    
    width: 80%;
    margin-bottom: 10px;
    border-radius: 2px;
}

h1,
h2,
h3,
p {
    font-family: courier;
    /*Ger utrymme mellan element*/
    margin-top: 20px;
    text-align: center;
}
</style>
