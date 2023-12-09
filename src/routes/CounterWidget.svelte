<script lang="ts">
	import Counter from './Counter.svelte';
	export let dateStr: string;
	export let countDownTitle: string;
	export let removeFromList: (counterTitle: string) => void;
</script>

<div class="counterContainer">
	<h1>Count Down to {countDownTitle}</h1>
	<button on:click={() => removeFromList(countDownTitle)} />
	<Counter {dateStr} />
</div>

<style>
	.counterContainer {
		list-style: none;
		border-radius: 1.5rem;
		border-color: var(--color-theme-2);
		border-style: solid;
		margin: 1rem;
		padding: 1rem;
		position: relative;
	}

	.counterContainer button {
		position: absolute;
		top: 0.5rem;
		right: 0.5rem;
		background-color: white;
	}

	.counterContainer button::before {
		content: '❌';
	}
</style>
