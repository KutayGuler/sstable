<script lang="ts">
	import TreeNode from './TreeNode.svelte';
	export let node: { value: number; l: any; r: any } | null;
</script>

{#if node}
	<div class="relative flex flex-col items-center space-y-2 text-xs">
		<!-- Node circle -->
		<div class="rounded-full bg-gray-100 px-3 py-0.5 text-gray-800 shadow">
			{node.value}
		</div>

		<!-- Connector lines to children -->
		{#if node.l || node.r}
			<div class="relative flex h-2 w-full justify-center">
				<!-- Vertical line down from parent -->
				<div class="absolute top-0 h-full border-l border-gray-300"></div>

				<!-- Horizontal line connecting to children -->
				<div class="absolute top-1/2 w-full border-t border-gray-300"></div>
			</div>
		{/if}

		<!-- Children container -->
		<div class="flex justify-center gap-4">
			<TreeNode node={node.l} />
			<TreeNode node={node.r} />
		</div>
	</div>
{/if}
