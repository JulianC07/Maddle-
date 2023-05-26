<script lang="ts">
  import WordEntry from './components/WordEntry.svelte'
  import PhraseFinder from './components/PhraseFinder.svelte';
  import LetterGrid from './components/LetterGrid.svelte';
  import Info from './components/Info.svelte';
  import Timer from './components/Timer.svelte';
  let targetCount = 4
  let timerStatus = 'ended'
  let level = 1
  let score = 0
  let duration = 60;
  let loser;
  function onTimerComplete () {
     timerStatus = 'ended'
    if (score >= targetCount) {
      level += 1
      targetCount += 4+Math.round(Math.random()*14)
    } else {
      //level = 1
      //score = 0
      loser = true;
    }
  }
  function resetGame () {
    level = 1;
    score = 0;
    loser = false;
  }
  
  function scoreUp (number = 1) {
    score += number
  }

  function onStart () {
    duration += 1;
    timerStatus = 'running'
  }

  

  
</script>

<main>
  
    
<header>
  Word Game
  <Info/>
</header>
  <h1>
    Maddle
  </h1>
  <h3>By Julian Castro</h3>

  <div>
    <Timer duration={duration} status={timerStatus} onComplete={onTimerComplete}/>
  </div>
  <br>
<div class = "level"> Level: {level} </div>  
  
  {#if loser}
   <h1 class = "Loser"> YOU LOSE LOSER </h1>
<button class = "StartAgain" on:click={resetGame}>Start over</button>
  {:else}
    
    <div>
      {#key level}
      <LetterGrid onScore={scoreUp}
        onStart = {onStart}
        />
      {/key}
    
    </div>
  {/if}
  <div class = "Target">
  Target: {targetCount}
</div>
    <div class= "scoreboard">
Score: {score}
</div>
</main>

<style>
  main {
    background-color: #2B2D42;
    color: white;
  }

  h1 {
border-top: 5px solid #EDF2F4;
    text-align: center;
font-family: 'DynaPuff', cursive;
    font-size: 60px;
    color: #D80032;

  }
  h3{
    text-align: center;
color: #EF233C;
border-bottom: 5px solid #EDF2F4;
font-family: 'DynaPuff', cursive;

  }
  header {
    display: flex;
	align-items:center;
		justify-content:space-between;
    color: #2B2D42;
    padding: 10px;
  }
    .scoreboard {
      font-family: 'DynaPuff', cursive;
    color: #D80032;
    font-size: 30px;
    border: 5px solid #8D99AE;
    width: 120px;
    padding: 5px;
    background: #EDF2F4;
    border-radius: 10%;
  
  }

  .level {
    font-family: 'DynaPuff', cursive;
      font-size: 30px;
    color: #8D99AE;
    background-color: #EDF2F4;
    width: 130px;
    border: 5px solid #8D99AE; 
  }

  .StartAgain {
     text-decoration: none;
    color: #EDF2F4;
      font-family: 'DynaPuff', cursive;
      font-size: 30px;
    background: black;
     border-radius: 10%;
      cursor: pointer;
  }
  .Target {
        font-family: 'DynaPuff', cursive;
      font-size: 25px;
    color: #8D99AE;
    background-color: #EDF2F4;
    width: 130px;
    border: 5px solid #8D99AE; 
  }
  .Loser {
    font-family: 'DynaPuff', cursive;
    animation-name: zoom;
    animation-duration: 3s;
    animation-iteration-count: infinite;
    bottom: 219px;
    font-size: 25px;
  }
  @keyframes zoom {
    0% {right: 0px; font-size: 100px; color: red;}
    50% {font-size: 25px; color: #2B2D42;}
    100% {font-size: 100px; left: 0px; color: red;}
    
  }
</style>
