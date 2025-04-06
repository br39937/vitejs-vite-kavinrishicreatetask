<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
  import Connect4 from './lib/Connect4.svelte'
  
  let player:number = 0
  let gridArray = Array(7).fill(null).map(() => Array(6).fill(null));// i used ai claude 3.7 on claude.ai to make this 2d array
  let storageArray = Array(7).fill(null).map(() => Array(6).fill(null));// this is a 2d array of 7 arrays of length 6

  storageArray.push(Array(7).fill(5))// dont consider this part of the 2d array but it is  an array that stores the height of the columns

  function changeCellColor(col: number, row: number, color: string) {
    if (gridArray[col][row]) {
        gridArray[col][row].update(color);
    }
  }
  function place(col:number,color: string){
    if(storageArray[7][col]>=0){
      let realcolor:string = "#00000"
      if(player == 0){
        player =1;
        realcolor = "#FF0000";
      }else{
        player = 0;
        realcolor = "#FFFF00"
      }
      changeCellColor(col, storageArray[7][col], realcolor);
      storageArray[7][col]-=1
    }

    
  }
</script>

<main>
  <div>
    <a href="https://vite.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>


  <div class="card">
    {#each Array(6) as _, row}
            {#each Array(7) as cell, col}
                <Connect4
                  key={`${row}-${col}`} 
                  row={row} 
                  col={col} 
                  fillColor={gridArray[col][row]?.fillColor || "#FFFFFF"}
                  bind:this={gridArray[col][row]} 
                  value={cell}/>
            {/each}
    {/each}
  </div>
    
  <button on:click={() => changeCellColor(1, 1, '#000000')}>Change [1][1] Text Color to Green</button>
  <button on:click={() => changeCellColor(2, 3, '#000000')}>Change [2][3] Text Color to Blue</button>
  <button on:click={() => changeCellColor(0, 0, '#000000')}>Change [0][0] Text Color to Red</button>

  <button on:click={() => place(0, '#000000')}>Row 1</button>
  <button on:click={() => place(1, '#000000')}>Row 2</button>
  <button on:click={() => place(2, '#000000')}>Row 3</button>
  <button on:click={() => place(3, '#000000')}>Row 4</button>
  <button on:click={() => place(4, '#000000')}>Row 5</button>
  <button on:click={() => place(5, '#000000')}>Row 6</button>
  <button on:click={() => place(6, '#000000')}>Row 7</button>


  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
