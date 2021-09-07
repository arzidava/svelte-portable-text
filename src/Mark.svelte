<script>
	import { getContext } from 'svelte';

	export let mark = '';
	export let child = {};

	const markDefs = getContext('markDefs');
	const serializers = getContext('serializers');

	$: markDef = markDefs.find((m) => m._key === mark) ?? {};

	$: ({ component, props } = serializers.has(mark)
		? serializers.get(mark)($$props)
		: serializers.get(markDef._type)($$props));
</script>

<svelte:component this={component} {...markDef} {...props}>
	{#if child.mark}
		<svelte:self {...child}>
			<slot />
		</svelte:self>
	{:else}
		<slot />
	{/if}
</svelte:component>
