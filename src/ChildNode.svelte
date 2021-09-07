<script>
	import { getContext } from 'svelte';
	import Mark from './Mark.svelte';

	export let _type = 'span';
	export let marks = [];
	export let text = '';

	const serializers = getContext('serializers');

	$: ({ component, props } = serializers.get(_type)($$props));
	$: mark = marks.reverse().reduce(
		(child, mark) => ({
			mark,
			child
		}),
		{}
	);
</script>

{#if marks.length}
	<Mark {...mark}>
		<svelte:component this={component} {...props}>{text}</svelte:component>
	</Mark>
{:else}
	<svelte:component this={component} {...props}>{text}</svelte:component>
{/if}
