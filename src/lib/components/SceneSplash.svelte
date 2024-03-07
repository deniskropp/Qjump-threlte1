<script>
	import { T, useTask } from '@threlte/core';
	import { Billboard, Stars, useTexture } from '@threlte/extras';
	import SceneBase from './SceneBase.svelte';

	let splash_z = 0;
	useTask((delta) => {
		splash_z += delta
	})

	const texture = useTexture('/splash.png');
</script>

<SceneBase />

<Stars />

{#await texture then value}
	<Billboard>
		<T.Mesh position={[0, 0, 0]} position.z={splash_z}>
			<T.MeshBasicMaterial map={value} alphaTest={0.5} transparent />
			<T.PlaneGeometry args={[7, 7]} />
		</T.Mesh>
	</Billboard>
{/await}
