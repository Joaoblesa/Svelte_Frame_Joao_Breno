<script>
  import { onMount } from "svelte";

  let nome = "API DOG";
  let busca = "";
  let listaRacas = [];

  onMount(async () => {
    try {
      const res = await fetch("https://dog.ceo/api/breeds/list/all");
      const json = await res.json();
      if (json.status === "success") {
        listaRacas = Object.keys(json.message);
      }
    } catch (e) {
      console.error("Erro ao carregar API:", e);
    }
  });

  $: filtrados = listaRacas.filter((r) =>
    r.toLowerCase().includes(busca.toLowerCase())
  );
</script>

<main>
  <h1 class="font-personalizada">Olá, {nome}!</h1>

  <div class="search-box">
    <input type="text" bind:value={busca} placeholder="Pesquisar raça..." />

    {#if busca.length > 0}
      <ul class="lista">
        {#each filtrados as raca}
          <li>
            <a href="/dog/{raca}">{raca}</a>
          </li>
        {/each}
      </ul>
    {/if}
  </div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 50px;
    font-family: "Inter", sans-serif;
    min-height: 100vh;
    background-color: #bee7ff;
  }

  .font-personalizada {
    color: #3700ff;
    font-weight: 800;
    font-size: 3rem;
    margin-bottom: 30px;
    letter-spacing: -1px;
  }

  .search-box {
    width: 100%;
    max-width: 400px;
  }

  input {
    width: 100%;
    padding: 15px 25px;
    border: 2px solid #9e8be6;
    border-radius: 30px;
    outline: none;
    font-size: 1rem;
    box-shadow: 0 4px 10px rgba(55, 0, 255, 0.1);
  }

  .lista {
    background: white;
    margin-top: 10px;
    padding: 0;
    border-radius: 15px;
    list-style: none;
    max-height: 250px;
    overflow-y: auto;
    border: 1px solid #9e8be6;
  }

  li a {
    display: block;
    padding: 12px 20px;
    text-decoration: none;
    color: #333;
    text-transform: capitalize;
  }

  li:hover {
    background-color: #f0f4ff;
  }
</style>
