<script>
	import { T, useTask } from '@threlte/core';
	import { Billboard, Stars, useTexture } from '@threlte/extras';
	import { interactivity } from '@threlte/extras';
	import { spring } from 'svelte/motion';

	interactivity();
	const scale = spring(1);
	let rotation = 0;
	//	useTask((delta) => {
	//		rotation += delta;
	//	});

	let splash_z = 0;
	useTask((delta) => {
		splash_z += delta
	})

	const texture = useTexture('/splash.png');
</script>

<T.PerspectiveCamera
	makeDefault
	position={[0, 0, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
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
	<Billboard>
		<T.Mesh position={[0, 0, 0]} position.z={splash_z}>
			<T.MeshBasicMaterial map={value} alphaTest={0.5} transparent />
			<T.PlaneGeometry args={[7, 7]} />
		</T.Mesh>
	</Billboard>
{/await}


<Stars />
