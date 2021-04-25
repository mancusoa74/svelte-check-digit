<script>
	import { fly } from 'svelte/transition';

	let cf = "";
	let len_cf = 0;
	let checksum = '';
	let sum_cf_char = 0;
	let tab_pari = {'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4, 'F': 5, 'G': 6, 'H': 7, 'I': 8, 'J': 9, 'K': 10, 'L': 11, 'M': 12, 'N': 13, 'O': 14, 'P': 15, 'Q': 16, 'R': 17, 'S': 18, 'T': 19, 'U': 20, 'V': 21, 'W': 22, 'X': 23, 'Y': 24, 'Z': 25, '0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9};
	let tab_dispari = {'A': 1, 'B': 0, 'C': 5, 'D': 7, 'E': 9, 'F': 13, 'G': 15, 'H': 17, 'I': 19, 'J': 21, 'K': 2, 'L': 4, 'M': 18, 'N': 20, 'O': 11, 'P': 3, 'Q': 6, 'R': 8, 'S': 12, 'T': 14, 'U': 16, 'V': 10, 'W': 22, 'X': 25, 'Y': 24, 'Z': 23, '0': 1, '1': 0, '2': 5, '3': 7, '4': 9, '5': 13, '6': 15, '7': 17, '8': 19, '9': 21};
	let tab_resto = {0: 'A', 1: 'B', 2: 'C', 3: 'D', 4: 'E', 5: 'F', 6: 'G', 7: 'H', 8: 'I', 9: 'J', 10: 'K', 11: 'L', 12: 'M', 13: 'N', 14: 'O', 15: 'P', 16: 'Q', 17: 'R', 18: 'S', 19: 'T', 20: 'U', 21: 'V', 22: 'W', 23: 'X', 24: 'Y', 25: 'Z'};
   
	$: {
		len_cf = cf.length;
		checksum = '';
	}

	function calcola_checksum() {
		console.log("compute checksum: " + cf);
		sum_cf_char = 0;
		for(let i = 0; i < cf.length; i++) {
			if (i % 2)
				sum_cf_char += tab_pari[cf[i]];
			else
				sum_cf_char += tab_dispari[cf[i]];
		}
		checksum = tab_resto[sum_cf_char % 26];
	}
</script>

<main>
	<h1>Calcolo checksum codice fiscale</h1>
	Codice Fiscale (15 lettere): &nbsp; <input bind:value={cf} placeholder='RSSMRA80A01L219' />
	
	{#if len_cf == 15}
		<button transition:fly="{{ x: 200, duration: 1500 }}" on:click={calcola_checksum}>Calcola Checksum</button> 
	{/if}
	
	{#if checksum}
		<p transition:fly="{{ y: 200, duration: 1500 }}"><span>La checksum del codice fiscale è: <b>{checksum}</b></span></p>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 100;
	}
	p {
		margin-top: 50px;
	}
	span {
		color: #2640d6;
		border: 5px solid rgb(95, 200, 24);
		padding: 10px;
		font-size: 2em;
		font-weight: 100;
	}	
</style>