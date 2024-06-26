<script>
	import Modal from './Modal.svelte'

	let person = 'miisingno';

	let showModal = false;

	$: full = `${person} Niger`;
	$: {
		console.log(person);
	}

	let dane = [
		{ name: 'Temperatura', value: 21, unit: '\u00B0', id: 1},
		{ name: 'Ciśnienie', value: 1013.5, unit: 'hPa', id: 2},
		{ name: 'Wilgotność', value: 69, unit: '%', id: 3},
	]

	function name(e)
	{
		person = e.target.value;
	}

	function ToggleModal()
	{
		showModal = !showModal;
	}

</script>

<Modal isPromo={true} show = {showModal} on:click={ToggleModal}>
	<!--<h3> Dodaj Nową Daną</h3>-->
	<form>
		<input type="text" placeholder="Dana">
		<input type="number" placeholder="Wartość">
		<input type="text" placeholder="Jednostka">
		<button> Dodaj Nową Daną</button>
	</form>
	<div slot="title">
		<h3>Dodaj Nową Daną</h3>
	</div>
</Modal>

<main>
	<!-- <h1>Hello {full}!</h1>
	<p>You Should Kill Yourself, NOW!</p>
	<input type="text" on:input={name} value={person}> -->

	<h1> Metealologia Website</h1>
	<button on:click|once={ToggleModal}> Włącz reklame </button>
	{#each dane as dana (dana.id)}
		<div>
			<h3>
				{dana.name}: {dana.value}{dana.unit}
				{#if dana.name == "Temperatura"}
					{#if dana.value > 25}
						<p style = "color: orange"> Ciepło</p> 
					{:else if dana.value < 15}
						<p style = "color: blue"> Zimno</p>
					{:else}
						<p style = "color: green"> Pogodnie</p>
					{/if}
				{:else if dana.name == "Ciśnienie"}
					{#if dana.value > 1018}
						<p style = "color: red"> Wysokie</p> 
					{:else if dana.value < 1010}
						<p style = "color: aqua"> Niskie</p>
					{:else}
						<p style = "color: green"> Idealne</p>
					{/if}
				{:else if dana.name == "Wilgotność"}
					{#if dana.value > 60}
						<p style = "color: darkblue"> Wysoka</p> 
					{:else if dana.value < 40}
						<p style = "color: beige"> Niska</p>
					{:else}
						<p style = "color: aquamarine"> Odpowiednia</p>
					{/if}
				{/if}
			</h3>
		</div>
	{:else}
		<p> coś sie chyba zepsuło</p>
	{/each}

</main>

<style>
	main {
	text-align: center;
	padding: 1em;
	max-width: 240px;
	margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>