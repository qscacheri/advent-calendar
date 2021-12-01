<script lang="ts">
	import Card from '../components/Card.svelte';
	import Snow from '../components/Snow.svelte';
	const cards = [
		1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25
	];

	let selectedDay = -1;
	let dayShouldWiggle = -1;
	function handleClick(day: number) {
		const cardDate = new Date(`12/${day}/2021`);
		const today = new Date();
		if (today >= cardDate) {
			selectedDay = day;
		} else {
			dayShouldWiggle = day;
			setTimeout(() => {
				dayShouldWiggle = -1;
			}, 1000);
		}
	}
</script>

<div class="page">
	<Snow />
	<div class="container">
		<h1>Boyd Advent Calendar</h1>
		<div class="card-container">
			{#each cards as card}
				<Card
					day={card}
					selected={selectedDay === card}
					on:click={() => handleClick(card)}
					wiggle={dayShouldWiggle === card}
				/>
			{/each}
		</div>
	</div>
</div>

<style>
	.page {
		position: relative;
	}
	h1 {
		color: gold;
		text-align: center;
		font-size: 3em;
		margin-top: 0;
		padding: 1rem;
	}
	.container {
		width: 100vw;
		height: 100%;
		display: flex;
		flex-direction: column;
		background: none;
		z-index: 2;
		position: relative;
		top: 0;
		left: 0;
	}

	.card-container {
		box-sizing: border-box;
		flex-grow: 1;
		display: grid;
		width: 100%;
		grid-template-columns: repeat(5, 1fr);
		grid-template-rows: repeat(5, 500px);
		gap: 1rem;
		padding: 1rem;
	}
	/* .image-container {
		position: absolute;
		top: 50vh;
		left: 50vw;
		transform: translate(-50%, -50%);
		width: 50vw;
		height: 50vh;
		background: purple;
	}
	.image-container img {
		max-height: 100%;
		width: auto;
	} */
</style>
