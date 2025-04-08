<script lang="ts">
	import TreeNode from './TreeNode.svelte';

	type Leaf = {
		value: number;
		r: Leaf | null;
		l: Leaf | null;
	};

	type Memtable = {
		root?: Leaf;
	};

	let memtable: Memtable = $state({});

	function generateRandomId() {
		return Math.floor(Math.random() * 9999);
	}

	function generateLeaf(value: number) {
		return {
			value,
			l: null,
			r: null
		};
	}

	function insertKey(key: number) {
		if (!('root' in memtable)) {
			memtable.root = generateLeaf(key);
			return;
		}

		let current = memtable.root as Leaf;

		while (true) {
			if (key === current.value) {
				// Optionally skip or handle duplicates
				return;
			}

			if (key < current.value) {
				if (current.l === null) {
					current.l = generateLeaf(key);
					return;
				}
				current = current.l;
			} else if (key > current.value) {
				if (current.r === null) {
					current.r = generateLeaf(key);
					return;
				}
				current = current.r;
			}
		}
	}
</script>

<main class="flex h-screen flex-col p-4">
	<button onclick={() => insertKey(generateRandomId())}>insert random key</button>
	<h1>Memtable</h1>
	<div class="h-full border border-black">
		{#if memtable.root}
			<TreeNode node={memtable.root} />
		{/if}
	</div>
</main>
