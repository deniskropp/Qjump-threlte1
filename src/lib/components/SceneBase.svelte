<script>
	import { T } from '@threlte/core';
</script>

<T.PerspectiveCamera
	makeDefault
	position={[0, 0, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
	}}
/>

<T.DirectionalLight position={[0, 10, 10]} />
