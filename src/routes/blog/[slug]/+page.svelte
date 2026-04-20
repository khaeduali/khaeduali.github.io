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
<div id="spacer"></div>

<style>
main {
    padding: 20px;
    width: 75vw;
    height: fit-content;
    margin: auto;
    display: flex;
}

#spacer {
    height: 300px;
    width: 1px;
    margin: auto;
    display: flex;
}

div {
    margin: auto;
}

* {
    color: #74c7ec;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    display: inline;
    /*Ger utrymme mellan element*/
    margin-top: 20px;
}

#title {
    font-size: 4em;
}

#date {
    margin-left: 30vw;
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
