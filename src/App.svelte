<script>
	let input = "Paste your text here";
	$: output = input
		.split("\n")
		.map((token) => token.split(" ").map(highlightFirstChars).join(" "));
	
	function highlightFirstChars(word) {
		if(!word) return "";
		let take = Math.ceil(word.length / 2);
		return '<span class="highlighted">' + word.slice(0, take) + "</span>" + word.slice(take);
	}
</script>

<h1>Bionic Reading</h1>
<p>Svelte app written by <a style="text-decoration: underline;" href="https://github.com/bttger">bttger</a></p>
<p>Inspired by <a style="text-decoration: underline;" href="https://github.com/crisanlucid/vite-react-tailwind-bionic-reading">crisanlucid's project</a></p>

<textarea rows="10" id="text-input" name="text-input" bind:value={input}></textarea>
{#each output as line}
	<p class="base">{@html line}</p>
{/each}

<style>
	#text-input {
		-webkit-box-sizing: border-box;
       -moz-box-sizing: border-box;
            box-sizing: border-box;
		width: 100%;
	}
	
	.base {
		white-space: normal;
		color: #636363;
		line-height: 1.5rem
	}
	
	:global(.base .highlighted) {
		color: #000;
		font-weight: bold;
	}
</style>