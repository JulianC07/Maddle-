<script>

  import LetterButton from './LetterButton.svelte';
  import {words, getWordsThatStartWith, isWord} from '../lists/words.ts';
  export let onScore 
export let onStart

  export let off = false;
  let wordCount = "abddd"
  let started = false;
  let word = ""
  let Astate="active"
  let letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
  let wordsFound = [
    
  ]
  let letterGrid = [
      [
    { state: 'active', letter: 'A' },
    { state: 'active', letter: 'B' },
    { state: 'active', letter: 'C' },
    { state: 'active', letter: 'D' },
    { state: 'active', letter: 'E' },
  ],
      [
    { state: 'active', letter: 'A' },
    { state: 'active', letter: 'B' },
    { state: 'active', letter: 'C' },
    { state: 'active', letter: 'D' },
    { state: 'active', letter: 'E' },
  ],
      [
    { state: 'active', letter: 'A' },
    { state: 'active', letter: 'B' },
    { state: 'active', letter: 'C' },
    { state: 'active', letter: 'D' },
    { state: 'active', letter: 'E' },
  ],
      [
    { state: 'active', letter: 'A' },
    { state: 'active', letter: 'B' },
    { state: 'active', letter: 'C' },
    { state: 'active', letter: 'D' },
    { state: 'active', letter: 'E' },
  ],
      [
    { state: 'active', letter: 'A' },
    { state: 'active', letter: 'B' },
    { state: 'active', letter: 'C' },
    { state: 'active', letter: 'D' },
    { state: 'active', letter: 'E' },
  ],
    ];
function getLetter () {
  let idx = Math.floor (
    Math.random()
    *
    letters.length
  );
  console.log(idx)
  
  return letters[idx]
}
  console.log('letter',getLetter())
  console.log('letter',getLetter())
  console.log('letter',getLetter())



  function resetGrid() {
    letterGrid.forEach(
      (row, rn) => {
        row.forEach((letterObject, cn) => {
          letterObject.letter=getLetter()
          letterObject.state='active'
        }
      )
      });
  }
  resetGrid()

    function resetWord() {
      word=''
      letterGrid.forEach(
      (row, rn) => {
        row.forEach((letterObject, cn) => {
          letterObject.state='active'
        }
      )
      });
      letterGrid = letterGrid; // force update
  }
  function change (ltr, rnChanged, cnChanged) {
    if (off) {
      change = "return";
    }
    console.log('Change!',ltr,rnChanged,cnChanged)
    letterGrid.forEach(
      (row, rn) => {
        row.forEach((letterObject, cn) => {
          if (rn==rnChanged&&cn==cnChanged) {
            letterObject.state="current"
          } else if (rn==rnChanged-1&&cn==cnChanged-1) { // top left
            letterObject.state = 'active';
          } else if (rn==rnChanged-1&&cn==cnChanged) { // top
            letterObject.state = 'active';
          } else if (rn==rnChanged-1&&cn==cnChanged+1) { // top right
            letterObject.state = 'active';
          } else if (rn==rnChanged&&cn==cnChanged-1) { // middle left
            letterObject.state = 'active';
          } else if (rn==rnChanged&&cn==cnChanged+1) { // middle right
            letterObject.state = 'active';
          } else if (rn==rnChanged+1&&cn==cnChanged-1) { // bottom left
            letterObject.state = 'active';
          } else if (rn==rnChanged+1&&cn==cnChanged) { // bottom middle 
            letterObject.state = 'active';
          } else if (rn==rnChanged+1&&cn==cnChanged+1) { // bottom right
            letterObject.state = 'active';
          } else {
            letterObject.state = 'inactive';
          }
        }
        )
      }
    )

    // Tell svelte to update
    letterGrid = letterGrid;
    word = word + ltr;
  }
    $: if (isWord(word)&&wordsFound.indexOf(word)==-1) {
        onScore()
       wordsFound=[...wordsFound,word];
    }

  $: if (word&&!started){
    onStart();
    started = true
  } 
</script>

<main>
  
  
  
  <button on:click={resetWord}>Reset</button>
  {#each letterGrid as row, rn}
    <div class ="row">
      {#each row as letterObject,cn}
    <LetterButton state={letterObject.state} 
      onPress={function (ltr) {change(ltr,rn,cn)}}
    letter={letterObject.letter}/>
      {/each}
    </div>
  {/each}

  <br>
  <div class="wordspelt">
  Word: {word}
  </div>
</main>

<style>
  main {
    --button-size: min(17vw,100px);
    position: relative;
  }
.row {
  display: flex;
  justify-content: center;
}

  .wordspelt {
     border: 5px solid #8D99AE;
      font-family: 'DynaPuff', cursive;
       width: 250px;
    font-size: 25px;
    color: #D80032;
    background: #EDF2F4;
     border-radius: 10%;
    margin: auto;
  
  }
  
  button {
 top: 0px;
    left: 0px;
    width: 100vw;
    height: calc(5*var(--button-size));
    text-decoration: none;
    color: #2B2D43;
      font-family: 'DynaPuff', cursive;
      font-size: 25px;
    background: transparent;
  border: none;
    position: absolute;
      cursor: pointer;

  }


</style>