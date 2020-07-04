<script>
    import * as PIXI from 'pixi.js'
    import {onMount} from "svelte";

    window.onresize = resize

    const appContainer = document.querySelector("#appContainer");
    const app = new PIXI.Application({
        antialias: true,
        transparent : true,
        resizeTo : window
    });
    app.view.style = "z-index : 99;"    // Set the overlay to be on top.

    const defaultLineStyle = {
        width : 2,
        color : 0xAA00BB,
        alpha : 1,
        cap : PIXI.LINE_CAP.ROUND
    }

    let anchors = calculateAnchors();

    const staticElements = [
        drawCrosshair,
        drawSpeedIndicator,
        drawFocusArea,
        drawBounds
    ];

    onMount(() => {
        document.querySelector("#appContainer").appendChild(app.view);
        anchors = calculateAnchors();
        staticElements.forEach((element) => element());
    });

    function calculateAnchors() {
        const side_bar_min_size = 300;
        const top_bar_min_size = 200;
        const bottom_bar_min_size = 200;
        const half_window_x = window.innerWidth/2;
        const half_window_y = window.innerHeight/2;
        const fifth_window_x = window.innerWidth/5;

        return {
            win_center_x : half_window_x,
            win_center_y : half_window_y,
            win_width : window.innerWidth,
            win_height : window.innerHeight,
            left_bar_bound : (fifth_window_x >= side_bar_min_size ? fifth_window_x : side_bar_min_size),
            right_bar_bound : (fifth_window_x >= side_bar_min_size ? fifth_window_x * 4 : window.innerWidth - side_bar_min_size),
            top_bar_bound : (fifth_window_x >= top_bar_min_size ? fifth_window_x : top_bar_min_size),
            bottom_bar_bound : (fifth_window_x >= bottom_bar_min_size ? fifth_window_x * 4 : bottom_bar_min_size)
        }
    }

    function drawSpeedIndicator() {
        const xcoord = window.innerWidth/4;
        const ycoord = 100;
        const radius = 50;
        const zeroDegrees = 1.5 * Math.PI;
        const twoSeventyDegrees = Math.PI;

        const arc = new PIXI.Graphics();

        arc.lineStyle(defaultLineStyle);
        arc.moveTo(xcoord, ycoord-radius);
        arc.arc(xcoord, ycoord, radius, zeroDegrees, twoSeventyDegrees);

        app.stage.addChild(arc);
    }

    function drawCrosshair() {
        const centerX = anchors.win_center_x;
        const centerY = anchors.win_center_y;

        const cross = new PIXI.Graphics();

        cross.lineStyle(defaultLineStyle);
        cross.moveTo(centerX-40, centerY)
            .lineTo(centerX+40, centerY)
            .moveTo(centerX, centerY-40)
            .lineTo(centerX, centerY+40);

        app.stage.addChild(cross);
    }

    function drawFocusArea() {
        const center_x = anchors.win_center_x;
        const center_y = anchors.win_center_y;
        const offset_x = 240;
        const offset_y = 180;
        const bracket_size = 30;

        const box = new PIXI.Graphics();

        box.lineStyle(defaultLineStyle);

        //top-left
        box.moveTo(center_x - offset_x, center_y - offset_y + bracket_size);
        box.lineTo(center_x - offset_x, center_y - offset_y);
        box.lineTo(center_x - offset_x + bracket_size, center_y - offset_y);

        //top-right
        box.moveTo(center_x + offset_x - bracket_size, center_y - offset_y);
        box.lineTo(center_x + offset_x, center_y - offset_y);
        box.lineTo(center_x + offset_x, center_y - offset_y + bracket_size);

        //bottom-right
        box.moveTo(center_x + offset_x, center_y + offset_y - bracket_size);
        box.lineTo(center_x + offset_x, center_y + offset_y);
        box.lineTo(center_x + offset_x - bracket_size, center_y + offset_y);

        //top-left
        box.moveTo(center_x - offset_x + bracket_size, center_y + offset_y);
        box.lineTo(center_x - offset_x, center_y + offset_y);
        box.lineTo(center_x - offset_x, center_y + offset_y - bracket_size);

        app.stage.addChild(box);
    }

    function drawBounds() {
        const bounds = new PIXI.Graphics();
        bounds.lineStyle(defaultLineStyle);

        console.log(anchors.right_bar_bound);

        bounds.moveTo(anchors.left_bar_bound, 0)
            .lineTo(anchors.left_bar_bound, anchors.win_height)
            .moveTo(anchors.right_bar_bound, anchors.win_height)
            .lineTo(anchors.right_bar_bound, 0);

        app.stage.addChild(bounds);
    }

    function resize() {
        anchors = calculateAnchors();

        app.stage.children.forEach((child) => child.clear());
        staticElements.forEach((element) => element());
    }
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

    /*.overlay canvas {*/
    /*    z-index: 99;*/
    /*}*/
</style>

<div id="appContainer" class="overlay">
</div>