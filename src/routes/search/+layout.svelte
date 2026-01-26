<script>
import {
    goto
} from '$app/navigation';

import { page } from '$app/stores';
	import { onMount } from 'svelte';
let searches = $state([])

onMount(()=> {
    if (searches.length == 0 && sessionStorage.getItem("searches").length >= 1)
        searches = JSON.parse(sessionStorage.getItem("searches"))
})

function handleSubmit(e) {
    e.preventDefault();
    const formData = new FormData(e.target);
    const search = formData.get('search');
    
    goto('/search/' + search).then(()=> {
        setTimeout(() => {
        if (!searches.some(obj=> obj.link == search) && $page.status == 200)
            searches.push({link: search, image: sessionStorage.getItem($page.params.pokemon+"_img")})
        if (searches.length > 5)
            searches.shift()
        sessionStorage.setItem("searches", JSON.stringify(searches))
        }, 1000);
    });
}
</script>

<div class="bg">

</div>

<main>
    <form onsubmit={handleSubmit}>
        <input type="text" name="search" placeholder="Sök upp en pokemon" />
    </form>
    <div style="height: 16px"></div>
    <slot>
    </slot>
</main>

<footer>
    <p style="display: inline">Senaste sökningar: </p>
    {#each searches as srch}
    <img src={srch.image} alt="pokemon" id="previewPokemon"><a href='/search/{srch.link}'>{srch.link}</a> <p style="display: inline">  </p>
    {/each}
</footer>

<style>
main {
    width: 80vw;
    height: 40vh;
    background-color: #11111baa;
    margin: 15vh auto;
    display: flex;
    padding: 16px;
    flex-direction: column;
    align-items: center;
    border-radius: 16px;
    border: #f5c2e7 2px solid;
}

footer {
    padding: 16px;
    width: 100vw;
    position: fixed;
    color: #f5c2e7;
    background-color: #11111b;
    font-family: courier;
    font-weight: bold;
    top: 0;
}

input {
    width: 70vw;
    margin: auto;
    height: 150%;
    padding: 2px 12px;
    border-radius: 16px;
    color: #f5c2e7;
    background-color: #11111b;
    border: #f5c2e7 2px solid;
    font-family: courier;
    font-weight: bold;
}

#previewPokemon {
    width: 30px;
    vertical-align: middle;
    height: 30px;
}

.bg {
    background-image: url("https://raw.githubusercontent.com/orangci/walls-catppuccin-mocha/master/city-horizon.jpg");
    width: 100vw;
    height: 100dvh;
    position: fixed;
    top: 0;
    left: 0;
    z-index: -1;
    filter: blur(15px) brightness(20%);
}

h1,
h2,
h3,
input,
p {
    font-family: courier;
    font-weight: bold;
    color: #f5c2e7;
}
</style>
