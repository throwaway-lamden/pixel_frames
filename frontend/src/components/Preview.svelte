<script>
    import { onMount } from 'svelte'
    import FrameCanvas from './FrameCanvas.svelte'
    import { frameSpeed, userAccount } from '../js/stores.js'
    import { isEmptyFrame, createWatermark } from '../js/utils.js'

    export let frames;
    export let thingInfo = false;
    export let pixelSize = 10
    export let showWatermark = true;
    export let border = true;

    let switcher;
    $: show = 1

    onMount(() => {
        if (thingInfo){
            switcher = setInterval(switchFrames, thingInfo.speed)
        }
        return(() => clearInterval((switcher)))
    })

    const switchFrames = () => {
        if (show > frames.length) show = 1
        else show = show === frames.length ? 1 : show + 1;
    }

    frameSpeed.subscribe(update => {
        if (!thingInfo){
            clearInterval((switcher))
            switcher = setInterval(switchFrames, update)
        }
    })

</script>

<style>
    .preview-frame{
        line-height: 0;
    }
    .preview-frame.border{
        border: 2px dashed #ff5bb0;
    }
</style>

<div class="preview-frame" class:border={border}>
    <FrameCanvas {pixelSize} pixels={frames[show - 1]} {thingInfo} watermark={showWatermark ? createWatermark(thingInfo, $userAccount) : undefined}/>
</div>