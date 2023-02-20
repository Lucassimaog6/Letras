<script>
	import Timer from '../components/Timer.svelte';
	import Input from '../components/Input.svelte';
	import LettersBox from '../components/LettersBox.svelte';
	let child;
	let timer;
	function grl() {
		child.generateRandomLetters();
		stop();
		restart();
	}
	function restart() {
		timer.restart();
	}
	function stop() {
		timer.stop();
	}
</script>

<main class="container h-full mx-auto flex flex-col gap-4 justify-center items-center">
	<Timer {grl} bind:this={timer} />
	<div class="flex gap-2 items-end">
		<Input {grl} />
		<button
			class="btn variant-filled-primary"
			on:click={() => {
				child.generateRandomLetters();
				stop();
				restart();
			}}>Gerar</button
		>
	</div>
	<LettersBox bind:this={child} />
</main>
