
<script>
  /** @type {import('./$types').PageData} */
  export let data;
</script>

{#await data}
  <p>.. waiting</p>
{:then pokemon} 
<article>
  {#each Object.entries(pokemon.response.sprites) as sprites}
    {#if typeof sprites[1] == "string"}
    <img src={sprites[1]} />
    {/if}
  {/each}
</article>
<h1>{pokemon.response.name.charAt(0).toUpperCase() + pokemon.response.name.slice(1)}</h1>
<section>

</section>

{/await}  


<style>
h1,
h2,
h3,
input,
p {
    font-family: courier;
    font-weight: bold;
    color: #f5c2e7;
}

article {
    display: flex;
    width: 90%;
    height: 50%;
    gap: .1em;
}
img {
    display: block;
    width: 100%;
    height: 100%;
}
</style>