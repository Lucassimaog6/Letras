<script>
	import { StoreLetters } from '../store';
	import Letter from './Letter.svelte';
	let randomLetters = '';
	export function generateRandomLetters() {
		randomLetters = [];
		for (let i = 0; randomLetters.length < 10; i++) {
			const newLetter = weightedRandom(itens, weights).item;
			if (randomLetters.indexOf(newLetter) === -1) {
				randomLetters.push(newLetter);
			}
		}
		StoreLetters.set(randomLetters);
	}
	const itens = [
		'a',
		'b',
		'c',
		'd',
		'e',
		'f',
		'g',
		'h',
		'i',
		'j',
		'k',
		'l',
		'm',
		'n',
		'o',
		'p',
		'q',
		'r',
		's',
		't',
		'u',
		'v',
		'w',
		'x',
		'y',
		'z'
	];

	const weights = [
		14.63, 1.04, 3.88, 4.99, 12.57, 1.02, 1.3, 1.28, 6.18, 0.4, 0.02, 2.78, 4.74, 5.05, 10.73, 2.52,
		1.2, 6.53, 7.81, 4.34, 4.63, 1.67, 0.01, 0.21, 0.01, 0.47
	];

	function weightedRandom(items, weights) {
		const cumulativeWeights = [];
		for (let i = 0; i < weights.length; i += 1) {
			cumulativeWeights[i] = weights[i] + (cumulativeWeights[i - 1] || 0);
		}
		const maxCumulativeWeight = cumulativeWeights[cumulativeWeights.length - 1];
		const randomNumber = maxCumulativeWeight * Math.random();
		for (let itemIndex = 0; itemIndex < items.length; itemIndex += 1) {
			if (cumulativeWeights[itemIndex] >= randomNumber) {
				return {
					item: items[itemIndex],
					index: itemIndex
				};
			}
		}
	}
</script>

<div class="grid grid-cols-10 gap-4">
	{#if randomLetters !== []}
		{#each randomLetters as rl}
			<Letter value={rl} />
		{/each}
	{/if}
</div>
