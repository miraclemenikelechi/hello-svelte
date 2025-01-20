<script lang="ts">
	import type { Snippet } from "svelte";

	interface props {
		name: string;
		children?: Snippet;
		nestedChildren?: Snippet;
	}

	let { name, children, nestedChildren }: props = $props();
</script>

<h1 class="text-5xl font-extrabold capitalize">{name}'s form</h1>

<!-- {@render children()} -->
