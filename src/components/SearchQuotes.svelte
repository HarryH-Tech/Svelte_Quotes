<script>
  import axios from "axios";
  let quotes = [];
  let query = "";
  let error = "";

  const searchQuotes = () => {
    axios
      .get(`https://api.quotable.io/search/quotes?query=${query}`)
      .then((res) => {
        console.log(res.data);
        quotes = res.data.results;
      })
      .catch((error) => {
        console.log(error);
        error = "Sorry, we failed to get the data, please try again.";
      });
  };
</script>

<div id="search-container">
  <input bind:value={query} type="text" id="search-input" />
  <br />
  <button on:click={searchQuotes}>Search</button>
</div>

{#if quotes.length > 0}
  <div class="grid">
    {#each quotes as quote}
      <div id="list-item-container">
        <h3>{quote.author}</h3>
        <p><i>"{quote.content}"</i></p>
      </div>
    {/each}
  </div>
{/if}

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

  #search-container {
    width: 50%;
    margin: 2rem auto;
    border: 4px solid black;
    border-radius: 0.6rem;
    text-align: center;
    padding: 0.6rem;
  }
</style>
