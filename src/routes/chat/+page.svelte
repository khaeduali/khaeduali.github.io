<script>
import {
    enhance
} from "$app";
import ElizaBot from 'elizabot';
const eliza = new ElizaBot();
let chat = $state([{
    user: 'Eliza',
    message: eliza.getInitial()
}]);

async function write(msg) {
    //TODO: Add the new message to the chat
    chat.append({user: 'User', message: msg});

    // random delay for Eliza's response time
    await new Promise((r) => setTimeout(r, 1000 + Math.random() * 1000));

    //TODO: Add Eliza's response to the chat
    chat.append({user: 'Eliza', message: eliza.transform(msg)})
}
</script>

<main>
    <section>
        {#each chat as msg}
        <article><p>{msg.message}</p></article>
        {/each}
    </section>
    <form  method="post"
        use:enhance={({ formElement, formData, action, cancel }) => {
        cancel(); //don't post anything to server
        const text = formData.get("text"); // what does "text" refer to?
        write(text);

        formElement.reset()

        }}>
        <input type="text" name="message" id="message" required placeholder="Send a message!">
    </form>
</main>

<style>
main {
    margin: auto;
    width: 60vw;
    height: 70vh;
    padding: 10px;
    background-color: #11111b;
    display: grid;
    grid-template: 90% 10% / auto;
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
    background-color: #181825;
    width: 90%;
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
 
.typing {
  animation-name: typing-anim;
  animation-duration: 3s; /* Längd på animationen (till exempel 3 sekunder) */
  animation-timing-function: ease-in-out; /* Funktion som styr tidsförloppet (till exempel "ease-in-out") */
}
               
 
@keyframes typing-anim {
    0% { color: #cdd6f4 }
    50% { color: #cba6f7 }
    100% { color: #cdd6f4 }
}

</style>
