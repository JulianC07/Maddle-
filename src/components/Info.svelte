<script>
  import {fade,fly} from 'svelte/transition'
let show = false;
</script>

<button on:click={()=>show=!show}>
	{#if show}
	
	{:else}
		
	{/if}
	?
</button>
{#if show}
<div class="fullscreen" in:fade out:fade>
	<button class="close" on:click={()=>
		show=false}>
		×
	</button>

  <div class="info" in:fly={{x:400,y:-400}}>
• Welcome to Maddle! The aim of the game is to make words under a certain amount of time. Each word counts as 1 point in the score. Don't try reusing the same word, it will not count as point since its already been used.
<br>
    <br>
• Need to create a new word? Simply just click around the grid to use another word!
<br>
<br>
• Once the timer ends the level will go up and reset the grid.
    <br>
    <br> 
• To check your score simply look at the bottom left corner of the game.
  <br>
    <br>
  • The bottom left corner also shows the word you are spelling.
    <br>
    <br>
    • If you make enough words for the target score continue to make words, your score will carry over to the next level to help you out!
	</div>
</div>
{/if}


<style>
button {
  width: 70px;
  height: 50px;
  font-family: 'DynaPuff', cursive;
  background-color: #EDF2F4;
  color: #EF233C;
  font-size: 20px;
    text-decoration: none;
    cursor: pointer;
font-size: 40px;
}
	.fullscreen {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		background-color: #2227;
		display: grid;
		place-content: center;

	}
	.info {
		padding: 8px;
		background-color: #2B2D42;
		color: #EDF2F4;
		box-shadow: 4px 4px #8D99AE;
		width: 80vw;
		height: 40vh;
    text-align: left;
		overflow-y: auto;
  font-family: 'DynaPuff', cursive;
    font-size: 25px;
	}
	.close {
		width: 2em;
		height: 2em;
		display: grid;
		place-content: center;
		border-radius: 50%;
		position: absolute;
		right: 4px;
		top: 4px;
	}


</style>