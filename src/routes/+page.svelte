<script lang="ts">
	import Header from './Header.svelte';

	type tStatus = 'OPEN' | 'CLOSE';

	let name: string = $state('trinity');

	let status: tStatus = $state('OPEN');

	function toggle() {
		status = status === 'OPEN' ? 'CLOSE' : 'OPEN';
	}
</script>

<div class="text-red-800">hello world</div>

<Header {name} />

<input type="text" bind:value={name} />

<p>the store is now {status}</p>
<button onclick={toggle}>toggle status</button>
