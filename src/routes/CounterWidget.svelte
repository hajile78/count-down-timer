<script lang="ts">
	import Counter from './Counter.svelte';
	export let dateStr: string;
	export let countDownTitle: string;
</script>

<div class="counterContainer">
	<h1>Count Down to {countDownTitle}</h1>
	<Counter {dateStr} />
</div>

<style>
	.counterContainer {
		list-style: none;
		border-radius: 1.5rem;
		border-color: var(--color-theme-2);
		border-style: solid;
	}
</style>
