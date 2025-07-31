<script>
	import { tick } from 'svelte';
	import gsap from 'gsap';

	import desk_01 from './tarte-catin/desk_01.jpeg';
	import desk_02 from './tarte-catin/desk_02.jpeg';
	import desk_03 from './tarte-catin/desk_03.jpeg';
	import desk_04 from './tarte-catin/desk_04.jpeg';

	import ext_01 from './tarte-catin/ext_01.jpeg';
	import ext_02 from './tarte-catin/ext_02.jpeg';
	import ext_03 from './tarte-catin/ext_03.jpeg';

	import one_hand_01 from './tarte-catin/one_hand_01.jpeg';
	import one_hand_02 from './tarte-catin/one_hand_02.jpeg';
	import one_hand_03 from './tarte-catin/one_hand_03.jpeg';

	import two_hands_01 from './tarte-catin/two_hands_01.jpeg';
	import two_hands_02 from './tarte-catin/two_hands_02.jpeg';
	import two_hands_03 from './tarte-catin/two_hands_03.jpeg';

	/**
	 * @param {HTMLElement} node
	 */
	function hero(node) {
		gsap.from(node, {
			ease: 'expo.out',
			duration: 4,
			opacity: 0,
			height: '50%',
			delay: 1
		});

		gsap.from(node.querySelector('h1'), {
			translateY: -10,
			ease: 'expo.out',
			opacity: 0,
			duration: 3,
			delay: 2
		});

		gsap.from(node.querySelector('img'), {
			ease: 'expo.out',
			duration: 3,
			delay: 1
		});
	}

	/** @type {HTMLElement|undefined} */
	let container = $state(undefined);
	let product = $state(false);
	let transition = false;

	async function toproduct() {
		if (!container || transition) return;
		transition = true;
		const tl = gsap.timeline({
			defaults: {
				ease: 'expo.inOut'
			}
		});

		tl.to(container, { scale: 0.9, duration: 1, ease: 'expo.out' });
		await tl.to(container, { translateX: '-100%', opacity: 0.2, duration: 2 });

		product = true;

		await tick();

		tl.set(container, {
			scale: 0.9
		});

		tl.from(container, {
			translateX: '100%',
			ease: 'expo.out',
			duration: 2
		});

		tl.to(container, {
			scale: 1,
			duration: 1
		});

		transition = false;
	}

	async function tohero() {
		if (!container || transition) return;
		transition = true;
		const tl = gsap.timeline({
			defaults: {
				ease: 'expo.inOut'
			}
		});

		tl.to(container, { scale: 0.9, duration: 1, ease: 'expo.out' });
		await tl.to(container, { translateX: '100%', opacity: 0.2, duration: 2 });

		product = false;

		await tick();
		transition = false;
	}
</script>

{#if product}
	<div class="container" bind:this={container}>
		<div class="product">
			<div class="top">
				<button onclick={tohero} aria-label="Revenir à la page d'accueil">
					<iconify-icon icon="fa6-solid:arrow-left"></iconify-icon>
				</button>

				<p class="primary-font title">Boisson Chaude</p>

				<button aria-label="Panier">
					<iconify-icon icon="fa6-solid:basket-shopping"></iconify-icon>
				</button>
			</div>

			<div class="img-container">
				<img src={two_hands_03} alt="" />
				<img src={desk_03} alt="" />
				<img src={one_hand_01} alt="" />
				<img src={ext_01} alt="" />
			</div>

			<div class="head">
				<h1 class="secondary-font">TARTE CATIN</h1>
				<div class="right">
					<div class="price">
						19<span>.90€</span>
					</div>
					<span class="leo">(gratuit pour Léonore)</span>
				</div>
			</div>

			<p>
				Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus non justo vel leo congue
				gravida. Donec egestas eu urna nec maximus. Nunc eget lobortis lorem, id sollicitudin
				libero. Aliquam erat volutpat. Donec in suscipit leo. Etiam scelerisque, nulla quis lacinia
				lacinia, enim metus consectetur elit, nec luctus metus nisi eget metus. Vestibulum
				scelerisque commodo volutpat.
			</p>
			<p>
				Suspendisse potenti. Praesent mattis quam sed ante ultricies, hendrerit pellentesque velit
				luctus. Duis molestie imperdiet ipsum sit amet volutpat. Nulla eget maximus diam. Nulla
				dictum lacus in metus euismod, eu fermentum tortor dapibus. Suspendisse potenti. Duis a
				ultrices diam. Nunc pretium mi massa, eget sodales erat mattis at. Nulla ac nisi ligula.
			</p>
			<p>
				Sed a lectus in magna varius euismod. In tempus libero quis erat egestas, vitae facilisis
				nunc finibus. Maecenas dignissim eros et lorem scelerisque, at egestas tortor cursus. Nam
				sagittis massa sed ullamcorper aliquam. Nunc imperdiet molestie magna sed pretium. Vivamus
				vestibulum cursus viverra. Sed turpis erat, cursus sed velit ac, tempor dignissim sem. Sed
				dignissim facilisis magna eget ornare. Duis volutpat dolor id nulla mollis, id pretium lacus
				condimentum. Proin placerat mauris vitae lacus elementum, eu ultrices lorem fringilla. Fusce
				hendrerit ex felis, at gravida ipsum consequat sit amet. Curabitur finibus, sem in imperdiet
				mollis, metus enim placerat lacus, eget feugiat sapien justo in ante. Etiam mollis vehicula
				nisi in finibus. Nulla eu dapibus purus. Suspendisse eu efficitur arcu.
			</p>
			<p>
				Curabitur vulputate, turpis et aliquet dictum, velit velit tempus arcu, vitae vehicula augue
				elit rhoncus metus. Etiam aliquet eros vitae arcu eleifend posuere. Maecenas convallis eros
				vel metus egestas ullamcorper. Vivamus dignissim ligula eget turpis auctor, fermentum
				pellentesque eros blandit. Pellentesque ornare libero a iaculis feugiat. Cras sed ultricies
				quam. Proin odio dui, lobortis non neque eu, feugiat venenatis enim. Aliquam eu cursus odio,
				eget mattis libero. Suspendisse maximus luctus dui, eu imperdiet risus eleifend eget.
				Praesent in tincidunt eros. Ut tempus purus a dapibus viverra. Suspendisse nisi ligula,
				venenatis eget odio cursus, pulvinar tincidunt libero.
			</p>
			<p>
				Duis quis nisi dignissim, eleifend urna sit amet, pulvinar eros. Pellentesque fringilla
				faucibus magna blandit facilisis. Proin volutpat risus id posuere vulputate. Nam dui nunc,
				efficitur vel magna a, egestas pharetra leo. Ut nec euismod enim. Pellentesque molestie
				sagittis rutrum. Proin in pulvinar eros, ac ullamcorper mi. Vivamus volutpat varius
				convallis. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia
				curae;
			</p>
		</div>
	</div>
{:else}
	<div class="container" bind:this={container}>
		<!-- svelte-ignore a11y_click_events_have_key_events -->
		<!-- svelte-ignore a11y_no_static_element_interactions -->
		<div class="hero" use:hero onclick={toproduct}>
			<div class="img">
				<img src={ext_03} alt="" />
			</div>
			<h1 class="secondary-font">TARTE CATIN</h1>
		</div>
	</div>
{/if}

<style lang="scss">
	:root {
		overflow: hidden;
	}

	.container {
		height: 100dvh;
		user-select: none;

		.product {
			position: relative;
			padding: 1rem;
			padding-bottom: 6rem;

			height: 100%;
			overflow: auto;

			.top {
				margin-bottom: 1rem;

				display: flex;
				justify-content: space-between;

				.title {
					font-size: 1.5rem;
					font-weight: 900;
				}
			}

			&::after {
				content: '';
				position: fixed;
				background: linear-gradient(to bottom, transparent, white);
				left: 0;
				right: 0;
				bottom: 0;

				height: 5rem;
			}

			.img-container {
				width: 100%;
				border-radius: 0.75rem;
				overflow: auto;

				display: flex;

				background-color: #eee;
				scroll-snap-type: x mandatory;

				img {
					flex-shrink: 0;
					width: 100%;
					height: 100%;
					object-fit: cover;

					scroll-snap-align: center;
				}
			}

			.head {
				display: flex;
				justify-content: space-between;
				margin-top: 1rem;
				margin-bottom: 2rem;

				h1 {
					line-height: 1;
				}

				.right {
					text-align: end;

					.price {
						font-size: 1.6rem;
						font-weight: 300;

						span {
							font-size: 0.6em;
							font-weight: 400;
						}
					}
				}
			}

			.leo {
				font-size: 0.8rem;
				font-style: italic;
				opacity: 0.5;
			}

			> p {
				margin-top: 1rem;
			}
		}

		.hero {
			height: 85%;
			margin: 1rem;
			position: relative;

			.img {
				width: 100%;
				height: 100%;
				border-radius: 0.75rem;
				overflow: hidden;
				pointer-events: none;

				img {
					width: 100%;
					height: 100%;
					object-fit: cover;
					border-radius: 0.75rem;

					scale: 1.5;
				}
			}

			h1 {
				position: absolute;
				bottom: 0;
				left: 50%;
				padding: 0.5rem 0.75rem;

				width: max-content;

				background-color: rgba(0 0 0 / 25%);
				backdrop-filter: blur(6px);

				border-radius: 0.5rem;

				font-size: 2rem;
				line-height: 1;
				text-align: center;

				color: white;

				translate: -50% 35%;
			}
		}
	}
</style>
