<script lang="ts">
  import WordEntry from './components/WordEntry.svelte'
  import PhraseFinder from './components/PhraseFinder.svelte';
  import LetterGrid from './components/LetterGrid.svelte';
  import Info from './components/Info.svelte';
  import Timer from './components/Timer.svelte';
  let targetCount = 4
  let timerStatus = 'ended'
  let level = 1
  let reset = 0
  let score = 0
  let duration = 60;
  let loser;
  let winner;
  function onTimerComplete () {
     timerStatus = 'ended'
    if (score >= targetCount) {
      reset += 1
      level += 1
      targetCount += 4+Math.round(Math.random()*14)
     winner = true;
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
    targetCount = 4;
    reset += 1 
    duration = 60;
  }
  
  function scoreUp (number = 1) {
    score += number
  }

  function onStart () {
    
    duration = 60 - level;
    timerStatus = 'running'
    winner = false;
  
  }

  console.log('test change')

  
</script>

<main>
  
    
<header>
  <h1>
   Maddle
  </h1>
  <h3>By Julian Castro</h3>
</header>
 

<div class = 'bar'>
  <div class='left'>
    <div>

     {#key reset} <Timer duration={duration} status={timerStatus} onComplete={onTimerComplete}/>{/key}
    </div>
    <div class = "level"> Level: {level} </div>  
  </div>
  <div class='right'>
    <div class = "Target">
  Target: {targetCount}
</div>
    <div class= "scoreboard">
Score: {score}
</div>
  </div>
</div>
  {#if loser}
   

   <h1 class = "Loser"> YOU LOSE LOSER </h1>
<button class = "StartAgain" on:click={resetGame}>Start over</button>
  {/if}

    <div>
      {#if winner}
     <h1 class = "Winner"> Level Up! </h1>
      {/if}
      {#key reset}
        <div class:invisible={loser}>
        <LetterGrid onScore={scoreUp}
          onStart = {onStart}
          />
        </div>
      {/key}
    
    </div>

  

  <footer>
    <Info/>
  </footer>
</main>

<style>
  .invisible {
    visibility: hidden;
  }
  main {
    display: flex;
    flex-direction: column;
    background-color: #2B2D43;
    color: white;
    min-height: 100vh;
  }

  footer {
margin-top: auto;

    text-align: right;
    padding: 8px;

  }

  h1 {

    text-align: center;
font-family: 'DynaPuff', cursive;
    font-size: 60px;
    color: #D80032;

  }
  h3{
    text-align: center;
color: #EF233C;

font-family: 'DynaPuff', cursive;

  }
  header {
    display: flex;
	align-items:center;
		justify-content: center;
    flex-direction: column;
    border-top: 5px solid #EDF2F4;
    border-bottom: 5px solid #EDF2F4;
    color: white;
    padding: 10px;
  }
    .scoreboard {
      font-family: 'DynaPuff', cursive;
    color: #D80032;
    font-size: 25px;
    border: 5px solid #8D99AE;
    width: 120px;
    padding: 5px;
    background: #EDF2F4;
    
  
  }

  .level {
    font-family: 'DynaPuff', cursive;
      font-size: 25px;
    color: #8D99AE;
    background-color: #EDF2F4;
    width: 130px;
    border: 5px solid #8D99AE; 
  }

  .Winner {
display: flex;
justify-content: center;
    margin-top: -82px;
    margin-bottom: 20px;
   border: none; 
animation-name: colors;
animation-duration: 2s;
animation-iteration-count: infinite;
    text-align: center;
    margin-left: 0px;
    margin-right: 0px;

  }

  .bar {
    display: flex;
    height: 90px;
    justify-content: space-between;
    align-items: flex-start;
  }

  .StartAgain {
     text-decoration: none;
    color: #EDF2F4;
      font-family: 'DynaPuff', cursive;
      font-size: 25px;
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
    position: absolute;
    font-family: 'DynaPuff', cursive;
    animation-name: zoom;
    animation-duration: 3s;
    z-index: 10;
    animation-iteration-count: infinite;
    bottom: 219px;
    width: 100%;
    text-align: center;
    font-size: 100px;
       border: none; 
  }

  @keyframes zoom {
    0% {transform:scale(1); color: red;}
    50% {transform: scale(0.25); color: #2B2D42;}
    100% {transform:scale(1); color: red;}
  }
  @keyframes colors {
    0% {color: red;}
    50% {color: yellow;}
    75% {color: green;}
    100% {color: red;}
  }

  @media screen and (max-width: 800px) {
   
    h1 {
     font-size: 25px;
    
    }
    h3{
      font-size: 15px;
    }
    .level {
      font-size: 17px;
      width: 80px;
    }
    .Target {
      font-size: 17px;
    } 
    .scoreboard {
      font-size: 17px;
    }
  .Winner {
display: flex;
justify-content: center;
    margin-top: 0px;

    }
  footer {
   padding-bottom: 5px;
  }
  }

</style>
