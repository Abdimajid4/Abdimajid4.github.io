<script>
    import { onMount, onDestroy } from 'svelte';
    import { writable } from 'svelte/store';
  
    const letters = ['A', 'B', 'C', 'D', 'E', 'F'];
    let pairs = [...letters, ...letters];
    let shuffledPairs = shuffleArray(pairs);
    let flippedCards = writable([]);
    let matchedPairs = 0;
    let timer;
    let seconds = writable(0);
  
    onMount(() => {
      timer = setInterval(() => {
        seconds.update(n => n + 1);
      }, 1000);
  
      return () => clearInterval(timer);
    });
  
    onDestroy(() => {
      clearInterval(timer);
    });
  
    function restartGame() {
      clearInterval(timer);
      seconds.set(0); // Reset the timer to 0
      pairs = [...letters, ...letters];
      shuffledPairs = shuffleArray(pairs);
      flippedCards.set([]);
      matchedPairs = 0;
    }
  
    function flipCard(index) {
      const cards = $flippedCards;
      if (!cards.includes(index) && cards.length < 2) {
        flippedCards.update(cards => [...cards, index]);
        setTimeout(checkMatch, 3000);
      }
    }
  
    function checkMatch() {
      const cards = $flippedCards;
      if (cards.length === 2) {
        const [index1, index2] = cards;
        if (shuffledPairs[index1] === shuffledPairs[index2]) {
          matchedPairs++;
          if (matchedPairs === letters.length) {
            clearInterval(timer);
            alert('You won! Play again!');
          }
          removeMatchedCards(index1, index2);
        }
        flippedCards.set([]);
      }
    }
  
    function removeMatchedCards(index1, index2) {
      shuffledPairs = shuffledPairs.filter((_, index) => index !== index1 && index !== index2);
    }
  
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    }
  </script>
  
  <style>
    .card {
      width: 100px;
      height: 100px;
      background-color: #ddd;
      margin: 5px;
      display: inline-block;
      cursor: pointer;
      text-align: center;
      line-height: 100px;
      font-size: 24px;
    }
  
    .matched {
      pointer-events: none;
      background-color: #ccc;
    }
  
    .flipped {
      background-color: #e351a2;
    }
  
    .letter {
      visibility: hidden;
    }
  
    .flipped .letter {
      visibility: visible;
    }
  </style>
  
  <main>
    {#each shuffledPairs as letter, index}
      <div class="card {$flippedCards.includes(index) && 'flipped'} {matchedPairs >= letters.length && 'matched'}"
           on:click={() => flipCard(index)}>
        <span class="letter">{letter}</span>
      </div>
    {/each}
  </main>
  
  <div>
    <button on:click={restartGame}>New Game</button>
    <p>Time: {$seconds}s</p>
  </div>
  