<script>
	import VideoReceiver from "./backdrop/VideoReceiver.svelte";
	import Overlay from "./overlay/Overlay.svelte";
	import HudOverlay from "./overlay/HudOverlay.svelte";
</script>

<style>
	:global(body) {
		overflow: hidden;
	}

	main {
		text-align: center;
		padding: 0px;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

<main>
	<VideoReceiver />
	<Overlay>
<!--		<TextMessageOverlay theText="Boebah ahahaaa!"></TextMessageOverlay>-->
		<HudOverlay />
	</Overlay>
</main>
