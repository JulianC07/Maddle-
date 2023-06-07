<script lang="ts">
  import {onDestroy} from 'svelte';
   let interval;
  export let status : 'running' | 'ended' = 'running';
  export let onComplete = ()=>{}
  export let duration : number = 5;
  let timerRunning = {}
  let gameOver = false;
  let now = window.performance.now();
  let start = window.performance.now();
  let elapsed = now - start;
  $: elapsed = now - start;
  $: if (elapsed > duration * 1000) {
    elapsed = duration * 1000;
    gameOver=true;
    status = 'ended';
    clearInterval(interval);
    onComplete()
  } else {
    gameOver = false;
  }

  function startTimer () {
  clearInterval(interval);
now = window.performance.now();
start= window.performance.now();
  interval = setInterval(
    ()=>now=window.performance.now(),
    -100
  )
}
  function stopTimer () {
		clearInterval(interval);
	}

  onDestroy(
  function () {
    clearInterval(interval);
  }
)

  $: {
    if (status=='running') {
      startTimer();
    } else if (status=='ended') {
      stopTimer();
    }
  }
  
</script>

<main>
    <div class ="time">
   Time left: {(duration - elapsed/1000).toFixed(2)}
  </div>

</main>

<style>
    button {
    text-decoration: none;
    color: #EDF2F4;
      font-family: 'DynaPuff', cursive;
      font-size: 30px;
    background: black;
     border-radius: 10%;
      cursor: pointer;
  }
  .time {
      font-family: 'DynaPuff', cursive;
      font-size: 25px;
    color: #8D99AE;
    background-color: #EDF2F4;
    width: 250px;
    border: 5px solid #8D99AE; 
  }
  .status {
  color:  #2B2D42;
  }
</style>
  