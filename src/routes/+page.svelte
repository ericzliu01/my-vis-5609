<script>
	let maxClick = $state(6);
	let cnt = $state(maxClick); // tip: https://svelte.dev/docs/svelte/$state

	function onClick() {
		// tip: Since DOM (i.e., the webpage content) will automatically update based on values, [<p id="info">Remaining Number of Clicks: {cnt}</p>]
		// we only need to change the cnt number here.
		if (cnt > 0) {
			cnt -= 1;
		}
	}
	$effect(() => {
		cnt = maxClick;
	});
</script>

<h1>Eric's VIS Site</h1>
<img
	width="200px"
	src="https://64.media.tumblr.com/6622e07314076cbf3f677abc87e5b7d5/a78bc1ad9ec7998a-02/s500x750/e59b86853a82300a6ba03ad72cef4dbcf2239722.jpg"
/>
<div>
	You can click up to
	<select bind:value={maxClick} onchange={() => (cnt = maxClick)}>
		{#each [2, 4, 6] as optionNum}
			<option value={optionNum}>
				{optionNum}
			</option>
		{/each}
	</select>
	times
</div>
<button onclick={onClick}> Click Me </button>

<!-- tip: use {#if...} template syntax here (https://svelte.dev/docs/svelte/if) so that the content below will automatically update when cnt value changes -->

{#if cnt > 0}
	<p id="info">Remaining Number of Clicks: {cnt}</p>
{:else}
	<p>No more clicks allowed</p>
{/if}

<style>
	body {
		font-family: Arial, Helvetica, sans-serif;
	}
	button {
		background-color: #44aa66;
		/* background-color: blue; */
		color: white;
		font-size: xx-large;
		padding: 10px 20px;
		border: none;
		cursor: pointer;
		border-radius: 5px;
	}
</style>
