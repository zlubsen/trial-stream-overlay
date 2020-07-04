<script>
    import {MediaPlayer} from "dashjs";
    import {onMount} from "svelte";
    import Overlay from "../overlay/Overlay.svelte";

    // let isFullScreen = document.fullscreenElement !== null;
    // console.log("fullscreen? -> " + isFullScreen);

    onMount(() => {
        // Sources: https://bitmovin.com/mpeg-dash-hls-examples-sample-streams/
        let url = "https://dash.akamaized.net/envivio/EnvivioDash3/manifest.mpd";
        // let url = "http://www.bok.net/dash/tears_of_steel/cleartext/stream.mpd";
        let player = MediaPlayer().create();
        player.initialize(document.querySelector("#videoPlayer"), url, true);
    });

    // function openFullscreen(element) {
    //     if (element.requestFullscreen) {
    //         element.requestFullscreen().catch(function (error) {
    //             console.log(error.message);
    //         });
    //     } else if (element.mozRequestFullScreen) { /* Firefox */
    //         element.mozRequestFullScreen();
    //     } else if (element.webkitRequestFullscreen) { /* Chrome, Safari & Opera */
    //         element.webkitRequestFullscreen();
    //     } else if (element.msRequestFullscreen) { /* IE/Edge */
    //         element.msRequestFullscreen();
    //     }
    // }
</script>

<style>
    video {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        -o-object-fit: cover;
        object-fit: cover;
        -o-object-position: center;
        object-position: center;
    }
</style>

<video id="videoPlayer" autoplay muted loop>
<!--    <source src="http://localhost:6000">-->
    Your browser does not support the video tag.
</video>
<!--{#if !isFullScreen}-->
<!--    <Overlay theText="Press F11 to Enter full screen mode" />-->
<!--{/if}-->