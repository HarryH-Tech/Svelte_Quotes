<script>
  import Loading from "./utils/Loading.svelte";
  import axios from "axios";
  import { onMount } from "svelte";
  let quote = [];
  let error = "";

  onMount(() => {
    axios
      .get("https://api.quotable.io/random")
      .then((res) => {
        console.log(res);
        quote = res.data;
      })
      .catch((error) => {
        console.log(error);
        error = "Sorry, we failed to get that data, please try again.";
      });
  });
</script>

{#if quote.length > 0}
  <div id="background">
    <div id="quote-container">
      <h4>{quote.author}</h4>
      -
      <p><i>"{quote.content}"</i></p>
    </div>
  </div>
{:else}
  <Loading />
{/if}

<style>
  #background {
    display: flex;
    justify-content: center;
    align-items: center;
    animation: color 4s infinite linear;
    height: 100vh;
  }

  #quote-container {
    background: linear-gradient(
      180deg,
      rgba(17, 255, 0, 0.582),
      rgba(0, 85, 255, 0.626)
    );
    backdrop-filter: blur(10px);
    border-radius: 0.6rem;
    border: 5px solid rgba(255, 255, 255, 0.6);
    box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.4);
    width: 70%;
    margin: auto;
    padding: 1rem;
    text-align: center;

    transition: all 0.5s ease-in-out;
  }

  #quote-container:hover {
    box-shadow: 10px 10px 32px 10px rgb(0, 0, 0);
  }

  h4,
  p {
    display: inline-block;
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
