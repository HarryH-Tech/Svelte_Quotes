<script>
import Header from "./components/Header.svelte"
import Home from "./components/Home.svelte"

export const answer = "42"
</script>

<p>This Paragraph</p>
<Header answer={answer}/>
<Home />


<style>
p {
	color: blue;
}
</style>