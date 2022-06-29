<script>
  import { Link } from "svelte-routing";
</script>

<div class="header">
  <h1>Quality Quotes</h1>

  <Link id="hi" to="/">Home</Link>
  <Link class="links" to="/quote-list">Quote List</Link>
  <Link class="links" to="/search-quotes">Search Quotes</Link>
</div>

<style>
  .header {
    background-color: #4477ff;
    padding: 1.5rem;
    text-align: center;
    color: white;
  }
</style>
