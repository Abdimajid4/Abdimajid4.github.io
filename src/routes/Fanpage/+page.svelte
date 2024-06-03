<script>
    let deck = [];
    let playerHand = [];
    let dealerHand = [];
    let playerScore = 0;
    let dealerScore = 0;
    let gameOver = false;
    let disabled = gameOver;

    function dealCards() {
        console.log("Dealing cards...");
        deck = [];
        playerHand = [];
        dealerHand = [];
        playerScore = 0;
        dealerScore = 0;
        gameOver = false;
        disabled = false; //makes Hit and Stand be pressed buttons
        const suits = ["Hjärter", "Spader", "Klöver", "Ruter"];
        const values = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A"];
        suits.forEach(suit => {
            values.forEach(value => {
                deck.push({ suit, value });
            });
        });

        for (let i = deck.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            const temp = deck[i];
            deck[i] = deck[j];
            deck[j] = temp;
        }
        playerHand.push(...deck.splice(0, 2));
        dealerHand.push(...deck.splice(0, 2)); // Bestämer hur många kort du får
        calculateScores();
        console.log("Player Hand:", playerHand);
        console.log("Dealer Hand:", dealerHand);
        console.log("Player Score:", playerScore);
        console.log("Dealer Score:", dealerScore);
    }

    function calculateScores() {
        playerScore = calculateScore(playerHand);
        dealerScore = calculateScore(dealerHand);
    }

    function calculateScore(hand) {
        let score = 0;
        let hasAce = false;
        hand.forEach(card => {
            if (card.value === "A") {
                hasAce = true;
            }
            score += getValue(card.value);
        });

        if (hasAce && score + 10 <= 21) {
            score += 10;
        }

        return score;
    }

    function getValue(value) {
        if (["J", "Q", "K"].includes(value)) {
            return 10;
        } else if (value === "A") {
            return 1;
        } else {
            return parseInt(value);
        }
    }

    function hit() {
        console.log("Player hits.");
        playerHand.push(deck.shift());
        calculateScores();
        console.log("Player Hand:", playerHand);
        console.log("Player Score:", playerScore);
        if (playerScore > 21) {
            console.log("Player busts!");
            gameOver = true;
            disabled = true; // Stopar Hit and Stand buttons
        }
    }

    function stand() {
        console.log("Player stands.");
        while (dealerScore < 18) {
            dealerHand.push(deck.shift());
            calculateScores();
        }
        console.log("Dealer Hand:", dealerHand);
        console.log("Dealer Score:", dealerScore);
        gameOver = true;
        disabled = true; // Stopar Hit and Stand buttons
    }
</script>

<style>
    .game-title {
        text-align: center;
        font-size: 24px;
        font-weight: bold;
        margin-bottom: 20px;
    }

    .card {
        border: 1px solid #000;
        width: 80px;
        height: 120px;
        display: inline-block;
        margin: 5px;
        text-align: center;
        font-size: 20px;
        font-weight: bold;
        border-radius: 10px;
        background-color: #e0e0e0;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        overflow: hidden;
        white-space: nowrap;
    }

    .card::after {
        content: '';
    }

    .card.red {
        background-color: #ff6666;
        color: #000000;
    }

    .card.black {
        background-color: #000000;
        color: #f91a0a;
    }

    button {
        background-color: #007bff;
        color: #d2336b;
        border: none;
        border-radius: 5px;
        padding: 10px 20px;
        margin: 5px;
        cursor: pointer;
        font-size: 16px;
        font-weight: bold;
    }

    button:disabled {
        background-color: #060303;
        color: #a74242;
        cursor: not-allowed;
    }

    h2 {
        margin-top: 20px;
        font-size: 24px;
        color: #740748;
    }

    h3 {
        margin-top: 10px;
        font-size: 20px;
        color: #007bff;
    }


</style>

<h1 class="game-title">Blackjack</h1>
<button on:click="{dealCards}">Deal</button>
<button on:click="{hit}" disabled="{disabled}">Hit</button>
<button on:click="{stand}" disabled="{disabled}">Stand</button>

<div>
    <h2>Player Hand</h2>
    {#each playerHand as card}
    <div class="card {card.suit === 'Hjärter' || card.suit === 'Ruter' ? 'red' : 'black'}">{card.value} {card.suit}</div>
    {/each}
    <p>Score: {playerScore}</p>
</div>

<div>
    <h2>Dealer Hand</h2>
    {#each dealerHand as card}
    <div class="card {card.suit === 'Hjärter' || card.suit === 'Ruter' ? 'red' : 'black'}">{card.value} {card.suit}</div>
    {/each}
    <p>Score: {dealerScore}</p>
</div>

{#if gameOver}
<h3>{playerScore > 21 ? "Player Busts!" : "Time is up"}</h3>
<h3>{playerScore <= 21 && (dealerScore > 21 || playerScore > dealerScore) ? "You Win" : "Dealer Wins"}</h3>
{/if}
