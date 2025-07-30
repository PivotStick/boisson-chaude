<script>
	import gsap from 'gsap';
	import { onMount } from 'svelte';

	const letters = [
		'A',
		'B',
		'C',
		'D',
		'E',
		'F',
		'G',
		'H',
		'I',
		'J',
		'K',
		'L',
		'M',
		'N',
		'O',
		'P',
		'Q',
		'R',
		'S',
		'T',
		'U',
		'V',
		'W',
		'X',
		'Y',
		'Z'
	];

	let currentLetter = $state(0);

	/**
	 * @param {HTMLElement} node
	 * @returns {import("svelte/transition").TransitionConfig}
	 */
	function a_in(node) {
		const anim = gsap.from(node, {
			opacity: 0,
			scale: 0,
			rotateX: 45,
			rotateY: 45,
			rotateZ: 45,
			translateZ: 80,
			ease: 'expo.out',
			duration: 3
		});

		return {
			duration: anim.duration() * 1000
		};
	}

	/**
	 * @param {HTMLElement} node
	 * @returns {import("svelte/transition").TransitionConfig}
	 */
	function a_out(node) {
		const anim = gsap.to(node, {
			opacity: 0,
			scale: 0,
			rotateX: 45,
			rotateY: -45,
			rotateZ: 45,
			translateZ: 80,
			ease: 'back.in',
			duration: 1
		});

		return {
			duration: anim.duration() * 1000
		};
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
		<div
			class="letter"
			in:a_in
			out:a_out
			onclick={() => (mounted = false)}
			onoutroend={() => {
				currentLetter = (currentLetter + 1) % letters.length;
				mounted = true;
			}}
		>
			{letters[currentLetter]}
		</div>
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
			cursor: pointer;
			user-select: none;

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
