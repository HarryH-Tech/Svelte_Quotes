<script>
  import axios from "axios";
  import Error from "./utils/Error.svelte";
  import Loading from "./utils/Loading.svelte";

  let quotes = [];
  let query = "";
  let error = "";
  let loading = false;

  const searchQuotes = () => {
    if (!query) {
      error = "Please enter a search query.";
      return;
    }
    error = "";
    loading = true;
    axios
      .get(`https://api.quotable.io/search/quotes?query=${query}`)
      .then((res) => {
        console.log(res.data);
        if (res.data.results.length === 0) {
          error = "No results found.";
          loading = false;
        } else {
          quotes = res.data.results;
          loading = false;
        }
      })
      .catch((error) => {
        console.log(error);
        error = "Sorry, we failed to get the data, please try again.";
        loading = false;
      });
  };
</script>

<div id="search-container">
  <input
    bind:value={query}
    on:focus={(error = "")}
    type="text"
    id="search-input"
  />
  <br />
  <button id="button" on:click={searchQuotes}>Search</button>
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

{#if error}
  <Error {error} />
{/if}

{#if loading}
  <Loading />
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
    width: 70%;
    margin: 2rem auto;
    text-align: center;
    padding: 0.6rem;
  }

  #search-input {
    border-radius: 1rem;
    padding: 0.4rem;
  }

  #button {
    background-color: #4477ff;
    color: white;
    border: none;
    border-radius: 0.6rem;
    padding: 0.6rem;
    font-size: 1.2rem;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
  }

  #button:hover {
    background-color: #33cccc;
    box-shadow: 5px 5px 5px #000;
  }

  #button:active {
    transform: translateY(8px);
  }
</style>
