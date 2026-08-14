<script lang="ts">
	import * as THREE from 'three';
	import { browser } from '$app/env';

	if (browser) {
		const { innerWidth, innerHeight } = window;

		const camera = new THREE.PerspectiveCamera(70, innerWidth / innerHeight, 0.01, 10);
		const scene = new THREE.Scene();
		const geometry = new THREE.BoxGeometry(0.2, 0.2, 0.2);
		const material = new THREE.MeshNormalMaterial();
		const mesh = new THREE.Mesh(geometry, material);
		const renderer = new THREE.WebGLRenderer({ antialias: true });

		function resize_renderer() {
			const { innerWidth, innerHeight } = window;
			renderer.setSize(innerWidth, innerHeight);
		}

		camera.position.z = 1;
		scene.add(mesh);
		resize_renderer();
		renderer.setAnimationLoop(animate);

		document.body.appendChild(renderer.domElement);
		window.addEventListener('resize', resize_renderer);

		function animate(time: number) {
			mesh.rotation.x = time / 2000;
			mesh.rotation.y = time / 1000;

			renderer.render(scene, camera);
		}
	}
</script>

<svelte:head>
	<meta charset="utf-8" />
	<title>My first three.js app</title>
	<style>
		body,
		html {
			margin: 0;
			overflow: hidden;
			background-color: #00000;
		}
	</style>
</svelte:head>
