<script lang="ts">
	export let day: number;
	export let selected: boolean;
	export let wiggle: boolean;
</script>

<div class="card" class:selected class:wiggle on:click>
	<!-- <img class="image" class:selected src={`/${day}.png`} alt="" /> -->
	<div class="image" class:selected />
	{#if !selected}
		<p class="day" class:selected>{day}</p>
	{/if}
</div>

<style>
	@keyframes wiggle {
		0% {
			transform: rotate(0deg);
		}

		10% {
			transform: rotate(5deg);
		}
		20% {
			transform: rotate(-5deg);
		}
		30% {
			transform: rotate(5deg);
		}
		40% {
			transform: rotate(0deg);
		}
	}
	.card {
		display: grid;
		place-items: center;
		width: 100%;
		height: 100%;
		background-color: blue;
		transition: all 0.2s ease-in-out;
		border-radius: 5px;
		color: gold;
		font-size: 3rem;
		cursor: pointer;
		overflow: hidden;
	}

	.card:nth-child(odd) {
		background: red;
	}
	.card:nth-child(even) {
		background: green;
	}
	.card.selected {
		transform: rotateY(180deg);
		background: gold;
		color: white;
	}
	.day {
		font-size: 8rem;
	}
	.day.selected {
		transform: rotateY(180deg);
		color: white;
	}
	.card.wiggle {
		animation: wiggle 1s;
	}
	.image {
		display: block;
		width: 100%;
		height: 100%;
		position: absolute;
		display: none;
		transition: all 0.2s ease-in-out;
	}
	.image.selected {
		display: block;
		position: static;
		background-image: url(/1.png);
		background-size: cover;
	}
</style>
