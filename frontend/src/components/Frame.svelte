<script>
    import { frames, currentFrame, totalPixels  } from '../js/stores'

    export let pixels
    export let pixelSize = 5
    export let frameNum = null;

</script>

<style>
    .board {
        position: relative;
    }
    .selected{
        border: 2px solid #b2d7b2;
    }
</style>

<div class="board"
     class:selected={frameNum !== null ? $currentFrame === frameNum : false}
     style={`grid-template-columns: repeat(16, ${pixelSize}px); grid-template-rows: repeat(16, ${pixelSize}px);`}
     on:click={() => currentFrame.set(frameNum)}>
    {#each pixels as pixel}
        <div class="pixel" style={`background: ${pixel}`} />
    {/each}

</div>