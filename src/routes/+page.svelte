<script>
	import { MiniCarousel, Image, VideoEmbed } from '$lib';

	export let data;
	
	$: ({ featured, carousels } = data);
</script>

<main>
	<ul class='galleries-layout'>
		{#each carousels as carousel}
			<li>
				<MiniCarousel {...carousel} />
			</li>
		{/each}
	</ul>
	{#if featured.image || featured.video}
		<section class='featured'>
			<a href='/whats-new'>
				<h3>what’s new</h3>
			</a>
			<div class='container'>
				<p>{featured.caption}</p>
				{#if featured.video}
					<VideoEmbed title='what’s new' url={featured.video} loop autoplay muted />
				{:else if featured.image}
					<Image src={featured.image} size={320} alt='what’s new' />
				{/if}
			</div>
		</section>
	{/if}
</main>

<style lang='scss'>
	main {
		width: 100%;
		margin: 0 auto;
		padding: 2rem 3rem;
		flex: 1;
		overflow: hidden;
		position: relative;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		.galleries-layout {
			flex: 1;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: flex-start;
			width: 100%;
			max-height: 100%;

			li {
				min-width: 12rem;
				max-width: 20rem;

				&:nth-child(1) {
					align-self: flex-end;
				}

				&:nth-child(2) {
					margin-top: 60vh;
					transform: translateY(-50%);
				}

				&:nth-child(3) {
					margin-top: 40vh;
					transform: translateY(-50%);
				}

				&:nth-child(4) {
					margin-top: 30vh;
					transform: translateY(-50%);
				}

				&:nth-child(5) {
					margin-top: 0;
				}
			}
		}

		@include lg {
			margin-top: 8rem;
			padding-left: inherit;
			padding: 1rem;
			overflow: visible;
			display: flex;
			flex-direction: column;
			align-items: center;

			.galleries-layout {
				display: flex;
				flex-direction: column;
				justify-content: flex-start;
				align-items: center;
				gap: 4rem;

				li {
					margin-top: 0 !important;
					transform: none !important;
					max-width: 20rem;

					&:nth-child(1) {
						align-self: inherit;
					}
				}
			}
		}

		.featured {
			position: absolute;
			bottom: 4rem;
			right: 3rem;

			h3 {
				font-family: 'supersize-bk-box', sans-serif;
				font-size: 1.2rem;
				color: $green;
				margin: 0.5rem 0;
			}

			.container {
				display: flex;
				align-items: flex-end;
				width: 100%;
				max-width: 16rem;

				p {
					position: absolute;
					font-size: 0.9rem;
					text-align: right;
					max-width: 12rem;
					bottom: 0;
					left: 0;
					transform: translateX(calc(-100% - 2rem));
					color: grey;
					margin: 1rem;
				}
			}

			@include lg {
				position: relative;
				bottom: auto;
				right: auto;
				margin-top: 6rem;

				.container {
					flex-direction: column-reverse;
					align-items: flex-start;
					max-width: 24rem;

					p {
						position: relative;
						text-align: left;
						transform: none;
						margin: 0.5rem 0;
						max-width: none;
					}
				}
			}
		}
	}
</style>