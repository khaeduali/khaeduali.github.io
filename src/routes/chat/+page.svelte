<script>
import {
    enhance
} from "$app/forms";
import ElizaBot from 'elizabot';

import {
    onMount
} from 'svelte';
onMount(() => {
    let localChat = JSON.parse(localStorage.getItem("chat"));
    if (localChat !== null && localChat.length > 2)
        chat = localChat
});

const eliza = new ElizaBot();
let chat = $state([{
    user: 'Eliza',
    message: eliza.getInitial(),
    time: ""
}]);

async function write(msg) {
    
    chat.push({
        user: 'User',
        message: msg,
        time: new Date().getHours() + ":" + new Date().getMinutes()
    });

    var element = document.getElementById("visible");
    
    element.style.display = "flex"; 

    localStorage.setItem("chat", JSON.stringify(chat))
        
    await new Promise((r) => setTimeout(r, 1000 + Math.random() * 1000));

    chat.push({
        user: 'Eliza',
        message: eliza.transform(msg),
        time: new Date().getHours() + ":" + new Date().getMinutes()
    });

    element.style.display = "none";

    localStorage.setItem("chat", JSON.stringify(chat))
}

function clearChat() {
    localStorage.removeItem("chat")
    chat = [{
    user: 'Eliza',
    message: eliza.getInitial(),
    time: ""
}]
}
</script>

<main>
    <section>
        {#each chat as msg}
        <article class={msg.user}><p data-time={msg.time}>{msg.message}</p></article>
        {/each}
        <article id="visible">
            <span class="typing"></span>
            <span class="typing"></span>
            <span class="typing"></span>
        </article>
    </section>
    <form  method="post"
        use:enhance={({ formElement, formData, action, cancel }) => {
        cancel(); 
        const text = formData.get("message"); 
        write(text);

        formElement.reset()

        }}>
        <input type="text" name="message" id="message" required placeholder="Send a message!">
    </form>
<button on:click={clearChat()}>Clear Chat</button>
</main>

<style>
main {
    margin: auto;
    width: 60vw;
    height: 70vh;
    padding: 10px;
    border-radius: 16px;
    margin-top: 20px;
    background-color: #11111b;
    display: grid;
    grid-template: 90% 10% / auto;
}

button {
    background-color: #11111b;
    border: none;
    border-radius: 16px;
    width: 100px;
    margin-top: 20px;
    font-family: courier;
    font-weight: bold;
    color: #f38ba8;
    scale: 1;
    transition: scale 0.2s;
}

button:hover {
    scale: 1.1;
}

button:active {
    scale: 0.9;
}

section {
    width: 100%;
    height: 100%;
    overflow-y: scroll;
}

form {
    width: 100%;
    height: 100%;
}

input {
    width: 100%;
}

article,
input {
    margin: 10px;
    padding: 10px;
    border-radius: 10px;
    background-color: #1e1e2e;
    width: 90%;
    transition: background-color 0.2s;
}

article:first-child {
    background-color: #181825;
}

article:hover {
    background-color: #313244;
}

h1,
h2,
h3,
input,
p {
    font-family: courier;
    font-weight: bold;
    color: #cdd6f4;
}

input {
    width: 95%;
    border: #b4befe00 2px dashed;
    transition: border-color 0.2s;
}

input::placeholder {
    font-weight: lighter;
    font-style: italic;
    opacity: 0.5;

}

input:focus {
    border-color: #b4befe;
}

.User {
    margin-left: 5%;
}

.User p {
    text-align: end;
    color: #89b4fa;
}

.User p::before {
    content: "User\a";
    font-style: italic;
    white-space: pre;
    color: #b4befe;
    opacity: 0.5;
    font-weight: lighter;
}

.User p::after {
    content: "\a" attr(data-time);
    white-space: pre;
    font-size: 0.7em;
    color: #b4befe;
    opacity: 0.2;
    font-weight: lighter;
}

.Eliza {
    margin-right: 5%;
}

.Eliza p {
    color: #cba6f7;
}

.Eliza p::before {
    content: "Eliza\a ";
    font-style: italic;
    white-space: pre;
    color: #cdd6f4;
    opacity: 0.5;
    font-weight: lighter;
}

.Eliza p::after {
    content: "\a" attr(data-time);
    white-space: pre;
    font-size: 0.7em;
    color: #cdd6f4;
    opacity: 0.2;
    font-weight: lighter;
}

#visible {
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 60px;
    background-color: transparent;
    padding: 0px;
    display: none;
}

.typing {
    opacity: 1;
    height: 10px;
    width: 10px;
    margin: 4px;
    border-radius: 50%;
    background-color: #cdd6f4;
    animation-name: typing-anim;
    animation-duration: 1s;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;
}

.typing:nth-child(1) {
    animation-delay: 0ms;
}

.typing:nth-child(2) {
    animation-delay: 333ms;
}

.typing:nth-child(3) {
    animation-delay: 666ms;
}

@keyframes typing-anim {
    0% {
        background-color: #cdd6f4;
        transform: scale(1);
    }

    25% {
        transform: scale(1.3);
    }

    50% {
        background-color: #cba6f7;
        transform: scale(1.4);
    }

    100% {
        background-color: #cdd6f4;
        transform: scale(1);
    }
}
</style>
