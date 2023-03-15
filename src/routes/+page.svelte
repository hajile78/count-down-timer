<script lang="ts">
	import { onMount } from 'svelte';
	import Counter from './Counter.svelte';
	import CounterWidget from './CounterWidget.svelte';
	type Counter = {
		date: string;
		title: string;
	};

	export let newCounter: Counter = { date: '', title: '' };
	let counterList: Counter[] = [];

	function addTolocalStorage(counterList: Counter[]) {
		localStorage.setItem('counterList', JSON.stringify(counterList));
	}

	function addToList() {
		if (!newCounter.date) return;
		counterList = [...counterList, newCounter];
		addTolocalStorage(counterList);
		newCounter = { date: '', title: '' };
	}

	export function removeFromList(counterTitle: String) {
		counterList = counterList.filter((item) => item.title !== counterTitle);
		addTolocalStorage(counterList);
	}

	onMount(() => {
		const defaultList = [
			{ date: '2023-05-12', title: 'Put-In-Bay' }
		];
		let local = localStorage.getItem('counterList');
		counterList = local === null ? defaultList && defaultList : JSON.parse(local);
		addTolocalStorage(counterList)
	});
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
	{#each [...counterList].sort((a, b) => a.date > b.date ? 1 : -1) as counter}
		<CounterWidget dateStr={counter.date} countDownTitle={counter.title} {removeFromList} />
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
</style>
