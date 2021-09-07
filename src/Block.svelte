<script>
	import { getContext, setContext } from 'svelte';
	import ChildNode from './ChildNode.svelte';

	export let _type = 'block';
	export let children = [];
	export let markDefs = '';
	export let style = '';

	const serializers = getContext('serializers');

	$: ({ component, props } = serializers.get(_type === 'block' ? style : _type)($$props));

	setContext('markDefs', markDefs);
</script>

<svelte:component this={component} {...props}>
	{#each children as child}
		<ChildNode {...child} />
	{/each}
</svelte:component>
