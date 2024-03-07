<script lang="ts">
	import { useTask } from '@threlte/core';
	import SceneSplash from './SceneSplash.svelte';
	import SceneMenu from './SceneMenu.svelte';

	let activeScene = 'splash';
	let splashTime = 0;

	useTask((delta) => {
		if (activeScene === 'splash') {
			splashTime += delta;

			if (splashTime > 5) {
				activeScene = 'menu';
			}
		}
	});
</script>

{#if activeScene === 'splash'}
	<SceneSplash />
{/if}
{#if activeScene === 'menu'}
	<SceneMenu />
{/if}
