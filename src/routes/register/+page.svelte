<script>
import {
    users_store
} from "$lib/user";
import {
    goto
} from '$app/navigation';
let users = [];

import {
    onMount
} from 'svelte';
onMount(() => {
    /*Check if has more then 2 characters*/
    if ($users_store.length > 2) {
        users = JSON.parse($users_store);
    }
});

let colors = [{
    color: "blue",
    name: "Blå"
}, {
    color: "red",
    name: "Röd"
}, {
    color: "green",
    name: "Grön"
}, {
    color: "black",
    name: "Svart"
}, {
    color: "white",
    name: "Vit"
}, {
    color: "purple",
    name: "Lila"
}, {
    color: "pink",
    name: "Rosa"
}, {
    color: "yellow",
    name: "Gul"
}]
let color = "black"
let username;
let email;
let pass;
let date;

function handleSubmit() {

    let new_user = {
        username: username,
        password: pass,
        email: email,
        date: date,
        color: color
    };

    if (pass.length < 8) {
        alert("Lösenordet måste vara 8 karaktärer eller mer!")
    } else if (users.filter(user => user.username === new_user.username).length > 0) {
        alert("Användarnamnet finns redan!")
    } else {
        users = [...users, new_user];
        $users_store = JSON.stringify(users);
        alert("Välkommen " + username + "!")
        goto("/")
    }
}
</script>

<main>
    <div class="container">
    <div class="container_offshoot" style="margin-top:-52vh; left: -1%;">
        <h1>Registrering</h1>   
    </div>
        <form class="formulär" on:submit|preventDefault={handleSubmit}>
            <label for="name">Namn</label>
            <input type="text" id="name"  bind:value={username}>
            <br>
            <label for="birth">Födelsedatum</label>
            <input type="date" id="birth" bind:value={date} >
            <br>
            <label for="email">E-Mail</label>
            <input type="email" id="email"  bind:value={email}>
            <br>
            <label for="pass">Lösenord</label>
            <input type="password" id="pass"  bind:value={pass}>
            <br>
            <label for="col">Favoritfärg</label>
            <select id="col" bind:value={color}>
                {#each colors as c}
                <option value={c.color}>{c.name}</option>
                {/each}
            </select>
            <div style="width: 80%; height: 20px; border-radius: 16px; overflow:hidden; background-color:{color}; margin-left: auto; margin-right: auto; margin-top: -17px; z-index:0;">    </div>
            <p></p>
            <input id="submitbutton" type="submit" value="Registrera" style="font-family: courier;">
        </form>

    <div class="container_offshoot">
        <sub>Har du redan ett konto? <a href="/login">Logga in!</a></sub>
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
    border: solid 5px #74c7ec;
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
    border: solid 5px #74c7ec;
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

    color: #74c7ec;
    font-family: courier;
    text-align: center;
    z-index: 2;
}

input {
    background-color: #181825;
    color: #74c7ec;
    border-color: #74c7ec;
    border-style: solid;

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

#col {
    font-family: courier;
    color: #74c7ec;
    border-color: #74c7ec;
    border-style: solid;

    background-color: #181825;
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    border-radius: 16px;
    z-index: 2;
    scale: 1;
    transition: scale 0.2s;
}

#col:hover {
    scale: 1.1;
}

#submitbutton {
    margin-top: 2%;
    font-size: 1em;
    height: 40px;
    font-weight: bolder;
    background-color: #74c7ec;
    border-color: #181825;
    color: #181825;
    border-style: solid;
}

h1,
sub {
    color: #74c7ec;
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
