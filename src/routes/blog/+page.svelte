<script>
	export let data;
  import { base } from '$app/paths';
</script>


<main>
<h1>Devblog</h1>

<ul>
	{#each data.posts as post}
		<li>
			<a href="{base}/blog/{post.slug}">
				{post.title} — {post.date}
			</a>
		</li>
	{/each}
</ul>
</main>

<style>

main {
  padding: 20px;
  width: 75vw;
  height: 75vh;
  margin: auto;
  display: flex;
  flex-direction: column;
}
div {
    margin: auto;
}

h1 {
    color: #74c7ec;
}

h2 {
    color: #b4befe;
    margin: auto;
}

h3, a {
    color: #cdd6f4;
    font-weight: bold;
}

h1,
h2,
h3,
p, a {
    font-family: courier;
    display: inline;
    /*Ger utrymme mellan element*/
    margin-top: 20px;
}

p sub {
    opacity: 0.5;
    font-size: small;
}

p strong {
    text-shadow: 0px 0px 4px #74c7ec72;
}

</style>