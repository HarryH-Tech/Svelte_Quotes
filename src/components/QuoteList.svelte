<script>
  import axios from "axios";
  import { onMount } from "svelte";

  let quotes = [];

  onMount(() => {
    axios
      .get("https://api.quotable.io/quotes")
      .then((res) => {
        console.log(res.data.results);
        quotes = res.data.results;
      })
      .catch((error) => {
        console.log(error);
        error = "Sorry, we failed to get the data, please try again.";
      });
  });
</script>

<div id="page-container">
  <h1>QUOTE LIST</h1>
  {#if quotes.length > 1}
    <div class="grid">
      {#each quotes as quote}
        <div id="list-item-container">
          <h3>{quote.author}</h3>
          <p><i>"{quote.content}"</i></p>
        </div>
      {/each}
    </div>
  {/if}
</div>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
    padding: 1rem;
  }

  #list-item-container {
    text-align: center;
    background: linear-gradient(
      180deg,
      rgba(17, 255, 0, 0.582),
      rgba(0, 85, 255, 0.626)
    );
    backdrop-filter: blur(10px);
    border-radius: 0.6rem;
    border: 5px solid rgba(255, 255, 255, 0.2);
  }

  h1 {
    text-align: center;
  }

  h3 {
    text-decoration: underline;
  }
</style>
