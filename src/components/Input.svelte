<script>
	import { StoreLetters } from '../store';
	let Letters;
	let status = '';
	let input_value = '';
	export let grl;
	let points = 0;

	StoreLetters.subscribe((value) => {
		Letters = value;
	});

	const verifyLetters = (_input_value) => {
		let is_valid = true;
		_input_value.split('').forEach((element) => {
			if (!Letters.includes(element)) {
				is_valid = false;
			}
		});
		return is_valid;
	};

	const verifyDictionary = async (_input_value) => {
		const response = await fetch(`https://dicio-api-ten.vercel.app/v2/${_input_value}`);
		if (response.status === 200) {
			return true;
		} else if (response.status === 400) {
			return false;
		}
	};

	const handleInput = async (e) => {
		if (e.key === 'Enter') {
			if (
				input_value.length >= 3 &&
				verifyLetters(input_value) &&
				(await verifyDictionary(input_value))
			) {
				console.log('Palava certa');
				grl();
				input_value = '';
				status_success();
				points++;
			} else {
				console.log('Palavra errada!');
				input_value = '';
				status_error();
			}
		}
	};

	const status_success = () => {
		status = 'success';
		setTimeout(() => {
			status = '';
		}, 500);
	};
	const status_error = () => {
		status = 'error';
		setTimeout(() => {
			status = '';
		}, 500);
	};
</script>

<div class="relative inline-block">
	<label class="label">
		<span>Digite sua palavra</span>
		<input
			class={`input input-${status.toString()}`}
			type="text"
			bind:value={input_value}
			on:keydown={(e) => handleInput(e)}
		/>
	</label>
	<span class="badge variant-filled-primary absolute -top-1 -right-1 z-10">Pontos: {points}</span>
</div>
