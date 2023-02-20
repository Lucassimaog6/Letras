<script>
	import Input from '../components/Input.svelte';
	import LettersBox from '../components/LettersBox.svelte';
	let child;
	function test() {
		child.generateRandomLetters();
	}
</script>

<main class="container h-full mx-auto flex flex-col gap-4 justify-center items-center">
	<div class="flex gap-2 items-end">
		<Input grl={test} />
		<button class="btn variant-filled-primary" on:click={child.generateRandomLetters}>Gerar</button>
	</div>
	<LettersBox bind:this={child} />
</main>
