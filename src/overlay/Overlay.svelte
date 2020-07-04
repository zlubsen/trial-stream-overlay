<script>
    import * as PIXI from 'pixi.js'
    import {onMount} from "svelte";

    // const container = document.querySelector("#container");
    // const hud_canvas = document.querySelector("#hud-overlay");
    // const app = new PIXI.Application({
    //     antialias: true,
    //     transparent : true,
    //     // view: hud_canvas,
    //     resizeTo : window
    // });
    // app.view.style = "z-index : 99;"


    let visible = document.fullscreenElement !== null;
    // let current = visible;


    function toggle() {
        console.log("toggle");
        visible = !visible;
    }
    // document.addEventListener('fullscreenchange', (event) => {
    //     // document.fullscreenElement will point to the element that
    //     // is in fullscreen mode if there is one. If there isn't one,
    //     // the value of the property is null.
    //     if (document.fullscreenElement) {
    //         console.log("ENTER full screen");
    //         visible = false;
    //     } else {
    //         console.log("EXIT full screen");
    //         visible = true;
    //     }
    // });
    //
    // onMount(() => {
    //     toggleVisible(visible);
    // });
    // function toggleVisible(isFull) {
    //     if (isFull) {
    //         console.log("visible: " + isFull);
    //         console.log("container hidden: " + document.querySelector("#container").hidden);
    //         document.querySelector("#container").setAttribute("hidden", !isFull);
    //     }
    // }

    // onMount(() => {
    //     document.querySelector("#container").appendChild(app.view);
    //
    //     const arc = new PIXI.Graphics();
    //
    //     arc.lineStyle(5, 0xAA00BB, 1);
    //     arc.arc(600, 100, 50, Math.PI, 2 * Math.PI);
    //
    //     app.stage.addChild(arc);
    // });
</script>

<style>
    .overlay {
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
    }

    /*.hidden {*/
    /*    display : none;*/
    /*}*/
</style>

<svelte:body
        on:fullscreenchange={toggle}
/>

<div id="container" class="overlay">
    <slot>
        <em>No overlay content was provided</em>
    </slot>
</div>