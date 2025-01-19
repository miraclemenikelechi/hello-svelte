<script lang="ts">
	let formState = $state({
		age: 0,
		error: "",
		isAdmin: false,
		name: "",
		step: 0
	});

	function progressFromStep1(): void {
		// basic validation step 1

		if (formState.name !== "") {
			formState.step += 1;
			formState.error = "";
		} else {
			formState.error = "name is empty or invalid";
		}
	}
</script>

<main class="h-screen text-white">
	<pre>
        {JSON.stringify(formState, null, 4)}
    </pre>

	<p>step: {formState.step}</p>

	{#if formState.step === 0}
		<div class="space-x-2">
			<label for="name">name</label>
			<input
				type="text"
				name="name"
				id="name"
				bind:value={formState.name}
				placeholder="name goes here"
			/>
		</div>

		<button onclick={progressFromStep1}>next</button>
	{:else if formState.step === 1}
		<div class="space-x-2">
			<label for="age">age</label>
			<input
				type="text"
				name="age"
				id="age"
				bind:value={formState.age}
				placeholder="age goes here"
			/>
		</div>

		<button
			onclick={() => {
				if (formState.age >= 18) {
					formState.step + 1;
					formState.error = "";
				} else {
					formState.error = "werey never enter 18";
				}
			}}>submit</button
		>
	{/if}
</main>

<style lang="scss">
	main {
		background-color: black;

		display: flex;
		align-items: center;
		justify-content: center;
		flex-flow: column;
	}

	input {
		color: black;
	}

	button {
		padding: 0.5rem 1rem;
		border: 1px solid rgba($color: #fff, $alpha: 100%);
	}
</style>
