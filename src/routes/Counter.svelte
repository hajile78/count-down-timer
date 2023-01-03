<script lang="ts">
	import { onMount } from 'svelte';
	export let dateStr: string;
	
	let goalDate = Date.parse(dateStr+'T00:00:00.000-04:00');
	let coundownDays: number;
	let days: number = 0,
		hours: number = 0,
		min: number = 0,
		seconds: number = 0;
	
	// console.log(`goalDate: ${goalDate} now: ${Date.parse(nowDate)}`)
	onMount(() => {
		const loop = () => {
			let nowDate = new Date
			coundownDays = goalDate - Date.parse(nowDate);
			days = Math.floor(coundownDays / (24 * 60 * 60 * 1000));
			hours = Math.floor((coundownDays - days * 24 * 60 * 60 * 1000) / (60 * 60 * 1000));
			min = Math.floor(
				(coundownDays - days * 24 * 60 * 60 * 1000 - hours * 60 * 60 * 1000) / (60 * 1000)
			);
			seconds = Math.floor(
				(coundownDays - days * 24 * 60 * 60 * 1000 - hours * 60 * 60 * 1000 - min * 60 * 1000) /
					1000
			);
			requestAnimationFrame(loop);
		};

		loop();
	});
</script>

<div class="counter">
	<strong>{new Date(goalDate).toLocaleDateString()}</strong>
	<div class="counter-viewport">
		<div class="counter-digits">
			<strong>{days} days {hours} hours {min} minutes and {seconds} seconds</strong>
		</div>
	</div>
</div>

<style>
	.counter {
		display: flex;
		border-top: 1px solid rgba(0, 0, 0, 0.1);
		border-bottom: 1px solid rgba(0, 0, 0, 0.1);
		margin: 1rem 0;
		text-align: center;
		flex-direction: column;
	}

	.counter {
		align-items: center;
		justify-content: center;
	}

	.counter-viewport {
		width: 42em;
		height: 4em;
		overflow: hidden;
		text-align: center;
		position: relative;
	}

	.counter-viewport strong {
		position: absolute;
		display: flex;
		width: 100%;
		height: 100%;
		font-weight: 400;
		color: var(--color-theme-1);
		font-size: 2rem;
		align-items: center;
		justify-content: center;
	}

	.counter-digits {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	/* .hidden {
		top: -100%;
		user-select: none;
	} */
</style>
