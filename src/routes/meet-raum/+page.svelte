<script>
    import Zoo from "$lib/zoo.svelte";
    import Footer from "$lib/footer.svelte";
    import { onMount } from "svelte";
    import { base } from "$app/paths";

    import raum_default from '$lib/assets/raum_default.png'
    import raum_closed from '$lib/assets/raum_closed.png'
    // yawn, roll, squint, meow, wave tail...
    // day/night?

    let states = $state([
        {
            "name":"initial",
            "description":"hello human!",
            "icon":"",
            "vis":0,
            "move":"false",
            "sound":"",
            "id":0
        }
    ]);
    let cidx = $state(0);
    let nStates = $state(0);

    let name = $derived(states[cidx].name);
    let desc = $derived(states[cidx].description);
    let icon = $derived(states[cidx].icon);
    let vis = $derived(states[cidx].vis);
    let move = $derived(states[cidx].move);
    let sound = $derived(states[cidx].sound);

    let visi = $state();
    let action = $state();
    let effect = $state();
    let isPet = false;
    let isPlay = false;
    let isFed = false;
    let ratio = $state();
    let stats = {
        'good':
        {'pet':0,
        'play':0,
        'fed':0
        },
        'bad':
        {'annoyed':0,
        'hungry':0}
    }

    onMount (function() {
        fetch(`${base}/raum_states.json`)
        .then(response => response.json())
        .then(data => {
            states = data;
            nStates = states.length;
        });

        rollAction();
        setInterval(rollAction, Math.floor(Math.random()*1000+4000));

        document.addEventListener('keydown', e=>{
            let key = e.key.toLowerCase();
            if (key === 'p') click();
            else if (key === 'l') play();
            else if (key === 'f') feed();
            else if (key === 's') console.log(stats);
        });
    });

    function rollAction() {
        if (!document) return;
        var statesHolder = document.querySelector('#conditions');

        if (name === 'hungry' && !isFed) stats.bad.hungry++;
        else if (name === 'playful' && !isPlay) stats.bad.annoyed++;
        else if (name === 'friendly' && isPet) stats.good.pet++;

        var rand;
        if (isPet && isPlay && isFed) rand = Math.floor(Math.random()*3)+2;
        else if (ratio < 0.4) rand = nStates-1;
        else rand = Math.floor(Math.random()*nStates);

        isPet, isPlay, isFed = false;

        cidx = rand;
        var nState = states[rand];
        var div = document.createElement('div');
        div.innerHTML += icon+' '+desc;
        statesHolder.prepend(div);
        div.classList.add('condition');

        var raum = document.getElementById('raum');
        switch (vis) {
            case 1:
                visi = raum_closed;
                break;
            default:
                visi = raum_default;
                break;
        }
        raum.src = visi;

        if (statesHolder.children.length > 5) 
            statesHolder.removeChild(statesHolder.lastChild);
    }

    function click() {
        action = 'you pet Raum\'s soft fur';
        var raum = document.getElementById('raum');
        raum.src = raum_closed;
        isPet = true;
        setTimeout(()=>{
            raum.src = visi;
        }, 500);
        if (name === 'irritated'){
            stats.bad.annoyed++;
            effect = 'The pet annoys Raum...';
        }
        else {
            stats.good.pet++;
            effect = 'Raum enjoys the pet!';
        }
    }

    function play() {
        isPlay = true;
        action = 'you play tag with Raum (leopards play by fighting, chasing, and hunting)';
        stats.good.play++;
        effect = 'Raum loves chasing the human!';
    }

    function feed() {
        isFed = true;
        action = 'you feed Raum an assortment of animals';
        stats.good.fed++;
        if (name === 'hungry') effect = 'Raum is delighted for food!';
        else effect = 'Raum enjoys the meal!';
    }

    $effect(()=> {
        console.log(action);
        console.log(effect);
        let goodVals = Object.values(stats.good);
        let badVals = Object.values(stats.bad);
        ratio = goodVals.reduce((x,cur)=>x+cur,0) / badVals.reduce((x,cur)=>x+cur,0);
    })
</script>

<style>
    #conditions {
        position: absolute;
        top: 65px;
        right: 0;
        overflow: hidden;
        mask: linear-gradient(to bottom, black 50%, transparent 90%);
        padding: 1rem 0;
        min-width: 20ch;
    }

    #conditions :global(.condition) {
        width: 90%;
        height: 3rem;
        border: 2px solid var(--cmain);
        border-radius: 1em;
        font-size: 1.4rem;
        padding: 2px 10px;
        background-color: hsla(0, 0%, 100%, .7);

        animation: new_item 400ms 70ms cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        transform: translate(-0.4em) rotateX(-90deg);
        transform-origin: top center;
    }

    @keyframes new_item {
        to {
            transform: none;
        }
    }

    #raum {
        position: absolute;
        bottom: 15%;
        left: 50%;
        transform: translateX(-50%);
        max-width: 100vw;
        transition: transform 200ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
        transform-origin: center bottom;
    }

    #raum:hover {
        transform: translateX(-50%) scale(0.96, 0.90);
    }

    #controls {
        position: fixed;
        top: 65px;
        left: 1rem;
        padding-top: 1rem;
        max-width: 50vw;
        flex-wrap: wrap;
    }

    #controls button {
        min-height: 3rem;
        min-width: fit-content;
        background-color: hsla(0,0%,0%,0);
        border: 2px solid var(--cmain);
        color: var(--cmain);
        border-radius: 2rem;
        transition: 200ms linear;
        padding: 0.2em 0.4em;
        font-size: 1.6rem;
    }

    #controls button:hover {
        color: var(--ccontrast);
        background-color: var(--camain);
    }

    #status {
        position: absolute;
        bottom: 4vh;
        left: 0;
        padding: 0.4rem 0.8rem;
        color: var(--ccontrast);
        font-size: 1.4rem;
        background-color: var(--catheme);
        border: 2px solid var(--ctheme);
        border-radius: 0 1em 1em 0;
        min-width: min(75ch, 80vw);
        width: 50vw;
        max-width: 50vw;
    }

    #status p {
        max-width: min(75ch, 80%);
    }

    #action::before {
        content: 'Action: ';
        font-weight: bold;
    }

    #effect::before {
        content: 'Effect: ';
        font-weight: bold;
    }

    @media screen and (min-width: 450px) {
        #controls {
            left: 50px;
        }
        #status {
            padding: 1rem 2rem;
            font-size: 2rem;
        }
    }

    @media screen and (min-width: 740px) {
        #conditions {
            min-width: fit-content;
            width: max(25vw, 25ch);
            max-width: max(25vw, 25ch);
        }
        #conditions :global(.condition) {
            width: 90%;
            height: 4rem;
            border: 2px solid var(--cmain);
            border-radius: 1em;
            font-size: 2rem;
            padding: 2px 10px;
        }
        #controls {
            padding-top: 2rem;
        }
        #controls button {
            height: 5rem;
            min-width: fit-content;
            background-color: hsla(0,0%,0%,0);
            border: 2px solid var(--cmain);
            color: var(--cmain);
            border-radius: 3rem;
            transition: 200ms linear;
            padding: 0.4em 0.8em;
            font-size: 2rem;
        }
        #status {
            padding: 1rem 2rem;
            width: 50vw;
            max-width: 50vw;
        }
    }

    @media screen and (min-width: 1200px) {
        #raum {
            bottom: 5%;
            width: 80vh;
            max-width: 80vw;
        }
        #controls {
            position: fixed;
            top: 65px;
            left: 50%;
            transform: translateX(-50%);
            padding-top: 2rem;
            width: 60vw;
            max-width: 60vw;
        }
        #controls button {
            height: 5rem;
            min-width: fit-content;
            background-color: hsla(0,0%,0%,0);
            border: 2px solid var(--cmain);
            color: var(--cmain);
            border-radius: 3rem;
            transition: 200ms linear;
            padding: 0.4em 0.8em;
            font-size: 2rem;
        }
    }
</style>

<svelte:head>
    <title>Raum | Amur Leopard | The Zoo</title>
</svelte:head>

<Zoo/>
<div class="parallax">
    <!-- cutouts of background -->
     <img class="object-cover h-screen min-w-screen" src="https://wwfeu.awsassets.panda.org/img/_c__natalia_kuksina__wwf_russia_1_643584.jpg" alt="forest">
     <img onclick={click} id="raum" class="" src={raum_default} alt="Raum">
</div>
<div id="conditions" class="flex flex-col w-1/5 h-2/5 max-h-100 flex flex-col items-center justify-start gap-5">
</div>
<div id="controls" class="flex flex-row gap-5 text-center">
    <button onclick={click} id="pet"><i class="fa-solid fa-computer-mouse"></i><i class="fa-solid fa-cat"></i>/<span class="public-sans-bold">P</span> | pet</button>
    <button onclick={play} id="play"><span class="public-sans-bold">L</span> | play</button>
    <button onclick={feed} id="feed"><span class="public-sans-bold">F</span> | feed</button>
    <button onclick={()=>console.log(stats)}><span class="public-sans-bold">S</span> | view stats in console</button>
</div>
<div id="status">
    <p id="action">{action}</p>
    <p id="effect">{effect}</p>
</div>
<div id="back">
    <a class="text-[2.4rem]" href="./" aria-label="Go Home"><i class="fa-solid fa-arrow-left"></i></a>
</div>
<Footer/>