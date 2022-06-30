<script>
  import axios from "axios";
  import { onMount } from "svelte";
  import Loading from "./utils/Loading.svelte";

  let quotes = [];
  let title = "hello";
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
  {:else}
    <Loading />
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
    border: 5px solid rgba(196, 106, 106, 0.429);
    border-radius: 1rem !important;
    animation: color 5s infinite linear;
    transition: all 0.5s ease-in-out;
  }

  h1 {
    text-align: center;
  }

  h3 {
    text-decoration: underline;
  }

  @keyframes color {
    0% {
      background: #33cccc;
    }
    20% {
      background: #33cc36;
    }
    40% {
      background: #b8cc33;
    }
    60% {
      background: #fcca00;
    }
    80% {
      background: #33cc36;
    }
    100% {
      background: #33cccc;
    }
  }
</style>
