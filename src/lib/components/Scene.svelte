<script>
	import { T, useTask } from '@threlte/core';
	import { useTexture } from '@threlte/extras';
	import { interactivity } from '@threlte/extras';
	import { spring } from 'svelte/motion';

	interactivity();
	const scale = spring(1);
	let rotation = 0;
	useTask((delta) => {
		rotation += delta;
	});

	const texture = useTexture('/splash.png');
</script>

<T.PerspectiveCamera
	makeDefault
	position={[10, 10, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 1, 0);
	}}
/>

<T.DirectionalLight position={[0, 10, 10]} />

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

{#await texture then value}
	<T.Mesh rotation.y={1}>
		<T.PlaneGeometry args={[5, 5]} />
		<T.MeshBasicMaterial map={value} />
	</T.Mesh>
{/await}
