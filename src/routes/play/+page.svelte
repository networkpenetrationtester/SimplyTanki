<script lang="ts">
	import './page.css';
	import * as THREE from 'three';
	import { browser } from '$app/env';
	import GUIElement from '$lib/components/GUIElement.svelte';

	function range(length: number) {
		return new Array(length).fill(0).map((_, i) => i);
	}

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
			renderer.setPixelRatio(window.devicePixelRatio);
			camera.aspect = innerWidth / innerHeight;
			camera.updateProjectionMatrix();
		}

		camera.position.z = 1;
		scene.add(mesh);
		resize_renderer();
		renderer.setAnimationLoop(animate);
		renderer.domElement.style.position = 'absolute';

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
</svelte:head>

<div class="overlay">
	<!-- TODO: fix spacing between images -->
	<!-- TODO: place these in a grid column that doesn't wrap which dynamically resizes horizontally -->

	<GUIElement asset="386" alt="rank" />
	<GUIElement asset="204" alt="begin_xp" />

	{#each range(40) as i (i)}
		<GUIElement asset="207" alt="middle" />
	{/each}

	<GUIElement asset="210" alt="border" />

	{#each range(3) as i (i)}
		<GUIElement asset="207" alt="middle" />
	{/each}

	<GUIElement asset="213" alt="end_cry" />
</div>
