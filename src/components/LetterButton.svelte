<script lang="ts">
  export let letter
  export let state : 'active' | 'inactive' | 'current'
  export let onPress = (letter : string) => null;
  function fireClickCallback () {
    onPress(letter);
  }
</script>

  <button 
    disabled={state=='inactive'||state=='current'}
    class:inactive={state=='inactive'}
    class:current={state=='current'}
    class:active={state=='active'}
    on:click={fireClickCallback}
    >
    {letter}
  </button>


<style>
  @import url('https://fonts.googleapis.com/css2?family=DynaPuff&display=swap');
  button {
    position: relative;
    width: var(--button-size);
    height: var(--button-size);
    font-family: 'DynaPuff', cursive;
    color: white;
    font-size: 30px;
    border-radius: 50%;
    border: 5px solid #EDF2F4;
    transition-duration: 0.4s;
    background-color: #2B2D42;
      cursor: pointer;
    display: grid;
    place-content: center;
    
    
  }
  button:hover {
    background-color: green;
  }
  .inactive {
    background-color: #D80032;
  }
  .active {
    
  }
  .current {
    background-color: green;
  }
</style>
