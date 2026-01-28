<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  let raca = $page.params.raca;
  let fotoUrl = "";

  onMount(async () => {
    const res = await fetch(`https://dog.ceo/api/breed/${raca}/images/random`);
    const json = await res.json();
    fotoUrl = json.message;
  });
</script>

<main>
  <h1>{raca}</h1>

  {#if fotoUrl}
    <div class="card">
      <img src={fotoUrl} alt="Dog" />
    </div>
  {:else}
    <p>Carregando...</p>
  {/if}

  <a href="/">← Voltar</a>
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
  h1 {
    text-transform: capitalize;
    color: #3700ff;
    font-size: 3rem;
  }
  .card {
    background: white;
    padding: 15px;
    border-radius: 20px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  }
  img {
    max-width: 100%;
    max-height: 400px;
    border-radius: 10px;
  }
  a {
    margin-top: 20px;
    text-decoration: none;
    color: #3700ff;
    font-weight: bold;
  }
</style>
