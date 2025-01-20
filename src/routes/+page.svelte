<script lang="ts">
	import Header from "./Header.svelte";

	interface iPerson {
		age: number;
		birthday: string;
		name: string;
	}

	interface iFormStepSnippet {
		id: string;
		question: string;
		type?: string;
	}

	interface iFormQuestion {
		question: string;
		id: string;
		type?: string;
	}

	interface iFormState {
		answers: iPerson;
		errors: Record<string, string>;
		isAdmin: boolean;
		step: number;
	}

	const initialFormState: iPerson = {
		age: 0,
		birthday: "",
		name: ""
	};

	let formState: iFormState = $state({
		answers: initialFormState,
		errors: {},
		isAdmin: false,
		step: 0
	});

	const formQuestions: iFormQuestion[] = [
		{
			id: "name",
			question: "what is your name"
		},
		{
			id: "age",
			question: "what is your age"
		},
		{
			id: "birthday",
			question: "when is your birthday",
			type: "date"
		}
	];

	function progressForm(id: keyof iPerson) {
		if (formState.answers[id]) {
			formState.step += 1;
			formState.errors[id] = "";
		} else {
			formState.errors[id] = `please the value for '${id}' is invalid. try again...`;
		}
	}
</script>

<main class="min-h-screen text-white">
	<Header name={formState.answers.name || "user"} />

	<p>step: {formState.step}</p>

	<!-- loop -->
	{#each formQuestions as { id, question, type }, index (id)}
		{#if formState.step === index}
			{@render formStep({ id, question, type })}
		{/if}
	{/each}

	<!-- component -->
	{#snippet formStep({ id, question, type = "text" }: iFormStepSnippet)}
		<article>
			<div>
				<label for={id}>{question}</label>
				<input {type} name={id} {id} bind:value={formState.answers[id as keyof iPerson]} />
			</div>

			<button onclick={() => progressForm(id as keyof iPerson)}>next</button>
		</article>
	{/snippet}

	<pre>
        {JSON.stringify(formState, null, 4)}
    </pre>
</main>

<style lang="scss">
	main {
		background-color: black;

		display: flex;
		flex-flow: column;
		gap: 1rem;
	}

	input {
		color: black;
	}

	button {
		padding: 0.5rem 1rem;
		border: 1px solid rgba($color: #fff, $alpha: 100%);
	}
</style>
