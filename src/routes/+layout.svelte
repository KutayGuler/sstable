<script module>
	interface Props {
		children?: import('svelte').Snippet;
	}
</script>

<script lang="ts">
	import '../app.css';
	let { children }: Props = $props();
</script>

{@render children?.()}
