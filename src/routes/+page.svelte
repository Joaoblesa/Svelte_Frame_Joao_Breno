<script>
  import { onMount } from "svelte";
  let busca = "";
  let listaRacas = [];

  onMount(async () => {
    const res = await fetch("https://dog.ceo/api/breeds/list/all");
    const json = await res.json();
    listaRacas = Object.keys(json.message);
  });

  $: filtrados = listaRacas.filter((r) => r.includes(busca.toLowerCase()));
</script>

<main>
  <h1 class="titulo">API DOG</h1>
  <input type="text" bind:value={busca} placeholder="Pesquisar raça..." />

  {#if busca}
    <ul class="lista">
      {#each filtrados as raca}
        <li><a href="/dog/{raca}">{raca}</a></li>
      {/each}
    </ul>
  {/if}
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 50px;
    font-family: sans-serif;
    background: #bee7ff;
    min-height: 100vh;
  }
  .titulo {
    color: #3700ff;
    font-weight: 800;
    font-size: 3rem;
  }
  input {
    width: 100%;
    max-width: 400px;
    padding: 15px;
    border-radius: 30px;
    border: 2px solid #9e8be6;
    outline: none;
  }
  .lista {
    background: white;
    width: 400px;
    border-radius: 15px;
    padding: 0;
    list-style: none;
    margin-top: 10px;
    border: 1px solid #9e8be6;
    overflow: hidden;
  }
  li a {
    display: block;
    padding: 10px 20px;
    text-decoration: none;
    color: #333;
    text-transform: capitalize;
  }
  li:hover {
    background: #f0f4ff;
  }
</style>
