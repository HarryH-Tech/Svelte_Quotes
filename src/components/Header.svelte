<script>
	let name = 'Sara';
	let src="https://picsum.photos/200/300";
 let count = 0;

    const incrementCount = () => {
        count += 1;
    }

    const double = () => {
        count *= 2;
    }

    $: doubled = count * 2;

    $: console.log("The count is " + count);
</script>

<h1>Hello {name.charAt(0)}!</h1>
<img {src} alt="{name}" />

<p>{@html count }</p>
<p>{@html doubled } </p>


{#if count > 10}
    <p>Count is greater than 10</p>
{/if}

<input placeholder="number..."/>
<button on:click={incrementCount}>count +</button>
<button on:click={double}>double</button>


<style>
	h1 {
		color: red;
	}
</style>