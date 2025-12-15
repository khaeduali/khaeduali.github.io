<script>
let images = [
    "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSZvrNgFklVW6-IXRy9XSMtO1j5eJJmHPcKfA&s",
    "https://img.freepik.com/free-vector/falling-poker-cards-aces-realistic-vector-icon-illustration_134830-2024.jpg?semt=ais_se_enriched&w=740&q=80",
    "https://cdn11.bigcommerce.com/s-spem6oukby/images/stencil/1280x1280/products/123/436/2D__57497__49826.1681470474.jpg?c=1",
    "https://img.lovepik.com/free-png/20210919/lovepik-credit-card-png-image_400515492_wh1200.png",
    "https://pngimg.com/d/cards_PNG8460.png",
    "https://pngimg.com/d/cards_PNG8471.png"
]

let redP = $state(0)
let blueP = $state(0)

let isBlueTurn = $state(false)

let canFlip = $state(true)

let cards = $state([])
start()

function start() {
    cards = []
    let unshuffledorder = []
    for (let i = 0; i < 12; i++)
        unshuffledorder.push(i)

    let order = unshuffledorder
    order = order.map(x => ({
        x,
        sort: Math.random()
    })).sort((a, b) => a.sort - b.sort).map(({
        x
    }) => x) // https://stackoverflow.com/questions/2450954/how-to-randomize-shuffle-a-javascript-array

    for (let i = 0; i < 12; i++) {
        cards.push({
            index: i,
            type: order[i] % 6,
            flipped: false,
            matched: false,
            celebrating: false
        });
    }
}

function reset() {
    start()
    canFlip = false;
    setTimeout(() => {
        canFlip = true;
    }, 1000);
}

function flip(card) {
    if (card.matched || !canFlip)
        return;

    let flippedAmt = 0;
    cards.forEach(c => {
        if (c.flipped && !c.matched) {
            flippedAmt++;
        }
    });

    if (flippedAmt < 2 || card.flipped) {
        card.flipped = !card.flipped;

        flippedAmt = 0;
        let matchedAmt = 0;
        cards.forEach(c => {
            if (c.flipped && !c.matched) {
                flippedAmt++;
            }
            if (c.matched) {
                matchedAmt++;
            }
        });
        if (flippedAmt > 1) {
            let otherCard = cards.find(c => c.flipped && c.index != card.index && !c.matched);

            if (otherCard.type === card.type) {
                otherCard.matched = true;
                card.matched = true;

                if (isBlueTurn)
                    blueP++;
                else
                    redP++;

                canFlip = false;
                setTimeout(() => {
                    otherCard.celebrating = true;
                    card.celebrating = true;
                }, 500);

                setTimeout(() => {
                    otherCard.celebrating = false;
                    card.celebrating = false;
                    canFlip = true;
                }, 1000);

                if (matchedAmt > 9) {
                    cards.forEach(_card => {
                        setTimeout(() => {
                            _card.celebrating = true;
                        }, 500);

                        setTimeout(() => {
                            _card.celebrating = false;
                        }, 1000);
                    });

                    setTimeout(() => {
                        isBlueTurn = blueP > redP
                    }, 500);
                }
            }

            setTimeout(() => {
                cards.forEach(c => {
                    c.flipped = c.matched;
                });
                if (matchedAmt <= 9)
                    isBlueTurn = !isBlueTurn;
            }, 1000);
        }
    }
}
</script>

<h1>Memory</h1>
<aside class={{'turnRed': !isBlueTurn}}>
</aside>
<aside class={{'turnBlue': isBlueTurn}}>
</aside>
<aside class="blue"><p>{blueP}</p>
    <div class="hat" id="blueHat"></div>
</aside>
<aside><p>{redP}</p>
    <div class="hat" id="redHat"></div>
</aside>
<main>
    {#each cards as card}
    <div class="card" class:flipped= { card.flipped } class:celebrating= { card.celebrating } class:notMatched= { !card.matched } on:click={()=>flip(card)}>
        <div class="cardimg">
            <img src={images[card.type]} alt="">
        </div>
        <div class="back">
            <img src="https://images.rawpixel.com/image_800/czNmcy1wcml2YXRlL3Jhd3BpeGVsX2ltYWdlcy93ZWJzaXRlX2NvbnRlbnQvbHIvdjExNDItMDE2YS1reW82cXVxZi5qcGc.jpg" alt="">
        </div>
    </div>
    {/each}
    <button type="button" on:click={()=>reset()}>⟳</button>
</main>

<style>
button {
    display: inline;
    width: 100%;
    font-size: 2em;
    font-weight: bolder;
    border: 2px dashed #74c7ec;
    border-radius: 16px;
    background-color: #11111b;
    color: #74c7ec;
    transition: all 0.1s;
}

button:hover {
    border-style: solid;
    border-width: 4px;
    scale: 1.1;
}

main {
    display: grid;
    justify-content: center;
    align-content: center;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(4, 100px);
    grid-gap: 20px;
}

@media (min-height: 500px) {
    main {
        grid-template-columns: repeat(4, 100px);
        grid-template-rows: repeat(3, 100px);
    }
}

@media (max-height: 500px) {
    main {
        grid-template-columns: repeat(6, 100px);
        grid-template-rows: repeat(2, 100px);
    }
}

aside {
    width: 100px;
    height: 100px;
    position: fixed;
    top: 240px;
    right: 10px;
    background-color: #11111b;
    color: #f38ba8;
    border-radius: 16px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.hat::before {
    content: '';
    /* Inget innehåll */
    width: 20px;
    height: 20px;
    position: fixed;
    background-color: whitesmoke;
    border-radius: 50%;
    /* Rundar kanter till en boll */
    margin-top: -20px;
    margin-left: -10px;
}

.hat {
    top: 145px;
    position: fixed;
    z-index: 3;
    width: 0px;
    height: 0px;
    border-bottom: 100px solid red;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
}

#redHat {
    transform: rotate(15deg);
    margin-left: 40px;
}

#blueHat {
    transform: rotate(-15deg);
    margin-right: 40px;
}

.hat::after {
    content: '';
    border-radius: 10px / 20px;
    margin-top: 90px;
    margin-left: -50px;
    width: 100px;
    height: 20px;
    z-index: 4;
    position: fixed;
    background-color: whitesmoke;
}

.blue {
    right: 0px;
    left: 10px;
    color: #74c7ec;
}

.turnBlue {
    top: 236px;
    left: 6px;
    right: 0px;
    box-shadow: 0 0 10px 10px #a6e3a122;
    border: 4px solid #a6e3a1;
    z-index: -1;
    opacity: 1;
    transition: all 0.4s;
}

.turnRed {
    top: 236px;
    right: 6px;
    box-shadow: 0 0 10px 10px #a6e3a122;
    border: 4px solid #a6e3a1;
    z-index: -1;
    opacity: 1;
    transition: all 0.4s;
}

p {
    font-size: 35px;
}

.card {
    position: relative;
    border: 2px dashed #74c7ec;
    border-radius: 16px;
    background-color: #11111b;
    transition: all 0.2s, opacity 1s 1s;
    opacity: 0.25;
}

.notMatched {
    opacity: 1;
}

.card img {
    position: absolute;
    border-radius: 16px;
    width: 100%;
    height: 100%;
}

.notMatched:hover {
    border-style: solid;
    border-width: 4px;
    scale: 1.1;
}

.cardimg img {
    transform: rotateY(180deg);
    transition: all 0.5s;
    transform-style: preserve-3d;
    backface-visibility: hidden;
}

.flipped .cardimg img {
    transform: rotateY(0deg);
}

.flipped .back {
    transform: rotateY(180deg);
}

.celebrating {
    scale: 1.4;
    background-color: #a6e3a1;
    border-color: #a6e3a1;
}

.back {
    position: absolute;
    background-color: #11111b;
    border-radius: 16px;
    width: 100%;
    height: 100%;
    transition: all 0.5s;
    transform: rotateY(0deg);
    backface-visibility: hidden;
    transform-style: preserve-3d;
}

.back img {
    opacity: 0.1;
}

h1 {
    margin-top: 20px;
    color: #74c7ec;
}

h1,
h2,
h3,
p {
    font-family: courier;
    text-align: center;
}
</style>
