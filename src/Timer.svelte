<script>
    import { createEventDispatcher } from "svelte";
    import ProgressBar from "./ProgressBar.svelte";
    const totalSeconds = 20;
    let secondLeft = totalSeconds;
    let isRunning = false;
    $: progress = ((totalSeconds - secondLeft) / totalSeconds) * 100;
    const dispatch = createEventDispatcher();
    function startTimer() {
        isRunning = true;
        const timer = setInterval(() => {
        secondLeft -= 1;
        if (secondLeft == 0) {
            clearInterval(timer);
            isRunning = false;
            secondLeft = totalSeconds;
            dispatch('end', "HANDS CLEAN!" )
        }
    }, 1000);

    }

   
</script>
<style>
        h2 {
        color: white;
        margin: 0;
    }
    .start {
        background-color: #93329e;
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled] {
        background-color: #b4aee8;
        cursor: not-allowed;
    }
</style>

<div bp="grid">
    <h2 bp="offset-5@md 4@md
    12@sm">
    Seconds Left:  {secondLeft}

    </h2>

</div>


<ProgressBar {progress} />

<div bp="grid">
    <button 
    disabled={isRunning}
    on:click={startTimer} 
    bp="offset-5@md 4@md
    12@sm" 
    class="start">
    Start
</button>


</div>

