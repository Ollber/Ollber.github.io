<script>
  let clicks = 0;
  let multiplier = 1;
  let workers = [];
  let worker_multiplier = 1;

  let upgrades = [
    { cost: 15, name: "Doubler", multiplier: 2, worker: 0 },
    { cost: 5, name: "Worker", multiplier: 0, worker: 1 },
    { cost: 1, name: "Cheat mode", multiplier: 10000, worker: 0 },
    { cost: 1, name: "Random mode", multiplier: -1, worker: 0 },

  ];

  function increment() {
    clicks = clicks + multiplier;
    console.log("click" + clicks);
  }
</script>


<article>
  <header>
    <div class="grid">
      {#each upgrades as upgrade}
        <button
          class="upgrade"
          on:click={() => {
            if (clicks >= upgrade.cost) {
              if (upgrade.multiplier) {
                multiplier = multiplier * upgrade.multiplier;
                clicks -= upgrade.cost;
              }
              if (upgrade.worker && clicks) {
                worker_multiplier = worker_multiplier * 2;
                workers = [upgrade.name, ...workers];
                /* start "clicking" every 1000 ms */
                setInterval(increment, 1000);
                clicks -= upgrade.cost;
              }
            } else {
              alert("Click some more first!");
            }
            
          }}
        >
          <span>{upgrade.name}</span>
          <span>{upgrade.cost * worker_multiplier}</span>
        </button>
      {/each}
    </div>
  </header>
  <div class="game">
    <button on:click={increment} class="clicker">
      <span class="clicks">{clicks}</span>
      <span class="pointtext">PPC: {multiplier}</span>
    </button>
  </div>
  <footer>
    <div class="panelright">
      <div>
    <div class="body">
      <div>
        <span>Workers</span>
        
        <div class="shop">
          {#each workers as worker}
            <div class="worker">{worker}</div>
          {/each}
        </div>
      </div>
      
    </div>
  </footer>
</article>

<style>

  article{
    background-color: rgba(0, 0, 0, 0);

  }

  footer{
    background-color: rgba(0, 0, 0, 0);

  }

  header{
    background-color: rgba(0, 0, 0, 0);

  }


  .shop {
    display: grid;
    grid-auto-flow: row; /* default */
    gap: 8px;
    grid-template-rows: repeat(3, 1fr);
    grid-template-columns: repeat(3, 1fr);
  }
  
  

  .upgrade {
    width: 100%;
    height: 100%;
    border: 4px solid rgb(0, 0, 0);
    background-color: rgb(0, 0, 0);
    background-size: cover;
    background-image: url("https://i.gifer.com/origin/46/46386bfd79c657009b6f30663a974e76.gif");
    place-items: center;
    place-content: center;
    display: flex;
    flex-direction: column;
  }

  .worker {
    width: 100%;
    height: 100%;
    border: 1px solid rgba(255, 255, 255, 0);
    background-color: rgb(24, 9, 111);
    place-items: center;
    place-content: center;
    display: flex;
  }

  .game {
    height: 50vh;
    display: flex;
    flex-direction: column;
    place-items: center;
    place-content: center;
  }
  .clicker {
    clip-path: circle();
    display: flex;
    height: 100%;
    width: 25%;
    flex-direction: column;
    place-items: center;
    place-content: center;
    background-image: url("https://pngimg.com/d/snowball_PNG6.png");
    
    background-position: -60px -17px;
  }

  .panelright {
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .clicks {
    font-size: 100px;
  }

  .pointtext {
    color: rgb(255, 255, 255);
    font-size: 40px;
    font-weight: bold;
  }
</style>
