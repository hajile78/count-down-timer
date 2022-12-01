<script lang="ts">
	import { onMount } from 'svelte';
	import CounterWidget from './CounterWidget.svelte';
	type Counter = {
		date: string;
		title: string;
	};

	export let newCounter: Counter = { date: '', title: '' };
	let counterList: Counter[] = []


	function addToList() {
		if (!newCounter.date) return;
		counterList = [...counterList, newCounter];
		localStorage.setItem('counterList', JSON.stringify(counterList))
		newCounter = { date: '', title: '' };
		console.log(counterList);
	}

	onMount(() => {
		
		const defaultList = [
			{ date: '2022-12-24T23:59:00Z', title: 'Christmas' },
			{ date: '2023-01-14', title: 'Red River Gorge' }
		]
		let local = localStorage.getItem('counterList')
		counterList = local === null ? defaultList : JSON.parse(local)
	})
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<form class="content" on:submit|preventDefault={addToList}>
		<label>
			date
			<input type="date" bind:value={newCounter.date} placeholder="YYYY-MM-DD" />
		</label>
		<label>
			title
			<input type="text" bind:value={newCounter.title} />
		</label>
		<button type="submit">Add new Counter</button>
	</form>
</section>

<section>
	{#each counterList as counter}
		<CounterWidget dateStr={counter.date} countDownTitle={counter.title} />
	{/each}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
