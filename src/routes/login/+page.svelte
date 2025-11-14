<script>
import {
    users_store
} from "$lib/user";
import {
    redirect
} from "@sveltejs/kit";
import {
    goto
} from '$app/navigation';

let users = []

import {
    onMount
} from 'svelte';
onMount(() => {
    /*Check if has more then 2 characters*/
    if ($users_store.length > 2) {
        users = JSON.parse($users_store);
    }
});

let email;
let pass;

function handleSubmit() {
    let login_user = {
        password: pass,
        email: email
    }

    let logged_users = users.filter(user => user.email == login_user.email && user.password == login_user.password);
    if (email == undefined || pass == undefined || email == "" || pass == "") {
        alert("Inget har blivit angivit!")
    } else if (logged_users.length > 0) {
        alert("Välkommen " + logged_users[0].username + "!")
        goto("/")
    } else {
        alert("Fel email eller lösenord!")
    }
}
</script>

<main>
    <div class="container">
        <h1>Inloggning</h1>
        <form class="formulär" on:submit|preventDefault={handleSubmit}>
            <label for="email">E-Mail</label>
            <input type="email" id="email"  bind:value={email}>
            <br>
            <label for="pass">Lösenord</label>
            <input type="password" id="pass"  bind:value={pass}>
            <p></p>
            <input type="submit" value="Logga in" style="font-family: courier;">
        </form>
    <div class="container_offshoot">
        <sub>Ny här? <a href="/register">Registrera!</a></sub>
    </div>
    </div>
</main>

<style>
main {
    min-width: 500px;
    min-height: 500px;
    width: 100%;
    height: 100%;
}

.container {
    border: solid 5px #b4befe;
    border-radius: 10px;
    width: 35%;
    min-width: 370px;
    height: 20%;
    min-height: 410px;
    background-color: #1e1e2e;
    margin: auto;
    margin-top: 10%;
    left: 30vw;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;
    position:absolute;
}
.container_offshoot {
    border: solid 5px #b4befe;
    border-radius: 10px;
    width: 100%;
    height: 5%;
    min-height: 60px;
    background-color: #1e1e2e;
    margin: auto;
    margin-top: 60vh;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-content: center;
    position:absolute;
}

label {
    font-weight: bold;
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

input {
    background-color: #313244;
    color: #b4befe;
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    border-radius: 16px;
    z-index: 2;
    scale: 1;
    transition: scale 0.2s;
}

input:hover{
    scale: 1.1;
}

h1,
sub {
    color: #b4befe;
    margin-left: auto;
    margin-right: auto;
}

h1,
h2,
h3,
sub,
p {
    font-family: courier;
}
</style>
