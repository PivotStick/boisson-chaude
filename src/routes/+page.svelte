<script>
	import gsap from 'gsap';
	import { onMount } from 'svelte';

	/**
	 * @param {HTMLElement} node
	 */
	function a(node) {
		const tl = gsap.timeline();

		tl.from(node, {
			opacity: 0,
			scale: 0,
			rotateX: 45,
			rotateY: 45,
			rotateZ: 45,
			translateZ: 80,
			ease: 'expo.out',
			duration: 3
		});
	}

	let mounted = $state(false);

	onMount(() => {
		setTimeout(() => {
			mounted = true;
		}, 1000);
	});
</script>

<div class="container">
	{#if mounted}
		<div class="letter" use:a>A</div>
	{/if}
</div>

<div class="copyright">#tarte-catin</div>

<style lang="scss">
	.container {
		display: flex;
		height: 100dvh;

		align-items: center;
		justify-content: center;

		.letter {
			font-weight: 900;
			font-size: 10rem;
			transform: perspective(8rem);
		}
	}

	.copyright {
		cursor: pointer;

		position: fixed;
		bottom: 0.5rem;
		right: 0.5rem;

		text-decoration: underline;
		font-style: italic;
		opacity: 0.5;
		font-size: 0.9rem;

		transition-property: opacity;

		&:hover {
			opacity: 1;
		}

		&:active {
			opacity: 0.25;
		}
	}
</style>
