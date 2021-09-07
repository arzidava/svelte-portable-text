<script>
	import { setContext } from 'svelte';
	import Block from './Block.svelte';
	import defaultBlocks from './defaultBlocks';

	export let blocks = [];
	export let serializers = {
		type: {},
		marks: {}
	};

	const blockTypes = {
		...defaultBlocks,
		...serializers.types,
		...serializers.marks
	};

	setContext('serializers', {
		has: (type) => blockTypes.hasOwnProperty(type),
		get: (type) => blockTypes[type]
	});
</script>

{#each blocks as block}
	<div><Block {...block} /></div>
{/each}
