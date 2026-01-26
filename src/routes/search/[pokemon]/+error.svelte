
<script>
  import { page } from '$app/stores';
</script>

<section>
  <h1>Error: {$page.params.pokemon}</h1>
  <hr />
  <h2>{$page.status}: {$page.error.message}</h2>
</section>
  

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
</style>