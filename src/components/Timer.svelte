<script>
	import { ProgressRadial } from '@skeletonlabs/skeleton';
	import { StorePoints } from '../store';
	let num = 100;
	let startInterval;

	export let grl;

	export function restart() {
		num = 100;
		startInterval = setInterval(() => {
			if (num > 0) {
				num -= 10;
			}
			if (num === 0) {
				timeout();
			}
		}, 1000);
	}

	function timeout() {
		StorePoints.update((num) => num - 1);
		grl();
	}

	export function stop() {
		clearInterval(startInterval);
	}
</script>

<div class="mb-5 w-40 aspect-square">
	<ProgressRadial font="100" value={num}>{num / 10}</ProgressRadial>
</div>
