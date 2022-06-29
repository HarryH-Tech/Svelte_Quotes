<script>
  import { Router, Route } from "svelte-routing";

  import Header from "./components/Header.svelte";
  import Home from "./components/Home.svelte";
  import QuoteList from "./components/QuoteList.svelte";
  import SearchQuotes from "./components/SearchQuotes.svelte";

  export let url = "";
</script>

<Router {url}>
  <Header />
  <Route path="/" component={Home} />
  <Route path="quote-list" component={QuoteList} />
  <Route path="search-quotes" component={SearchQuotes} />
</Router>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: Arial, Helvetica, sans-serif;
    cursor: url("http://www.javascriptkit.com/dhtmltutors/cursor-hand.gif"),
      auto;
  }
</style>
