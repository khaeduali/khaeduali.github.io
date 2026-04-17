<script>
  /** @type {import('./$types').PageData} */
  export let data;
</script>

<main>
<article>
  <h1 id="title">{data.title}</h1>
  <p id="date">Published: {data.date}</p>
  <svelte:component this={data.content} />
</article>
</main>

<style>

main {
  padding: 20px;
  width: 75vw;
  height: 75vh;
  margin: auto;
  display: flex;
}

div {
    margin: auto;
}

* {
    color: #74c7ec;
    font-family: courier;
    display: inline;
    /*Ger utrymme mellan element*/
    margin-top: 20px;
}


#title {
  font-size: 4em;
}

#date {
  margin-left: 40vw;
  color: gray;
}

p sub {
    opacity: 0.5;
    font-size: small;
}

p strong {
    text-shadow: 0px 0px 4px #74c7ec72;
}
</style>