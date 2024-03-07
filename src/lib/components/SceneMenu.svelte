<script>
	import { T, useTask } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { spring } from 'svelte/motion';
	import SceneBase from './SceneBase.svelte';

	interactivity();
	const scale = spring(1);
	let rotation = 0;
	useTask((delta) => {
		rotation += delta;
	});
</script>

<SceneBase />

<T.Mesh
	rotation.y={rotation}
	position.y={1}
	scale={$scale}
	on:pointerenter={() => scale.set(1.5)}
	on:pointerleave={() => scale.set(1)}
>
	<T.BoxGeometry args={[1, 2, 1]} />
	<T.MeshBasicMaterial color="hotpink" />
</T.Mesh>
