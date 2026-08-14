<script lang="ts">
	import type { $GUIElementConfig } from '$lib/types';
	let props: $GUIElementConfig = $props();
	const { asset, alt } = $derived(props);
</script>

<img src={'/resources/' + asset + '.png'} alt={alt ?? 'no alt text'} />
