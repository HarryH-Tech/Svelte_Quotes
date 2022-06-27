<script>
    import axios from "axios"
    import {onMount} from "svelte";
    let quotes = [];
    let corsProxy = "https://corsanywhere.herokuapp.com/"

    onMount(() => {
        axios.get("https://api.quotable.io/search/authors?query=einstein")
        .then(res => {
            
            console.log(res)
            quotes = res.data.results;
        }).catch(error => {
            console.log(error)
        })
    });
</script>

{#each quotes as quote}
    <p>{quote.bio}</p>
{/each}


<style>

</style>