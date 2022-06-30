<script>
  import { link } from "svelte-routing";
</script>

<div class="header">
  <h1>Quality Quotes</h1>

  <a href="/" class="links" use:link>Home</a>
  <a href="/quote-list" class="links" use:link>Quote List</a>
  <a href="/search-quotes" class="links" use:link>Search Quotes</a>
</div>

<style>
  .header {
    background-color: #4477ff;
    padding: 1.5rem;
    text-align: center;
    color: white;
  }

  .links {
    color: white !important;
    margin: 2rem;
  }

  @media (max-width: 600px) {
    .links {
      display: block;
    }
  }
</style>
