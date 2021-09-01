<script>
	import Fetcher from '../utils/fetcher';
	let isFirst = true;
	let isLoading = false;
	let data = [];
	const getPokemon = async (url) => {
		if (isLoading) return;
		isLoading = true;
		data = [];
		data = await fetch(url).then((res) => res.json());
		isFirst = false;
		console.log(data);
		isLoading = false;
	};
</script>

<div class="poke">
	{#if isFirst}
		<button on:click={() => getPokemon('https://pokeapi.co/api/v2/pokemon?limit=100&offset=200')}
			>Get Pokemon</button
		>
	{:else}
		<div class="action">
			<button on:click={() => getPokemon(data.previous)} disabled={isLoading}>Previous</button>

			<button on:click={() => getPokemon(data.next)} disabled={isLoading}>Next</button>
		</div>
	{/if}

	{#if isLoading}
		<div>Loading...</div>
	{/if}

	<div id="pokemon-list" class="pokemon-list" />
	{#if data.results}
		{#each data.results as pokemon}
			<ol class="list">
				<li class={`list ${pokemon.name}`}>
					<a href={pokemon.url}>
						{pokemon.name}
					</a>
				</li>
			</ol>
		{/each}
	{/if}
</div>

<style>
	.poke {
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		padding: 25px;
	}
	button {
		margin: 10px;
		padding: 10px;
		cursor: pointer;
		border: 0;
		box-shadow: 0 0 2px #000;
		border-radius: 0.5em;
		transition: transform 0.2s ease;
		max-width: 150px;
	}
	button:hover {
		transform: scale(1.1);
	}
	.pokemon-list {
		display: flex;
		flex-wrap: wrap;
		flex-direction: row;
	}
	ol {
		line-height: 2;
	}

	ol li {
		list-style-type: none;
		counter-increment: item;
		display: flex;
		align-items: center;
	}

	ol li a {
		text-decoration: none;
		text-transform: capitalize;
		color: #000;
	}

	ol li:before {
		content: '';
		display: inline-block;
		width: 12px;
		height: 20px;
		margin-right: 5px;
		background-color: #f9dd94;
		color: #7eb4e2;
		font-weight: bold;
		font-size: 140%;
		padding: 0 8px 8px;
		border-radius: 3px;
		line-height: 1.3;
	}
</style>
