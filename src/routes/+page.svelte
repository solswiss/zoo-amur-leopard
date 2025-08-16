<script>
    import Zoo from "$lib/zoo.svelte";
    import Header from "$lib/header.svelte";
    import Footer from "$lib/footer.svelte";
    import MeetTab from "$lib/meet_tab.svelte";
    import {base} from "$app/paths";
    import {onMount} from "svelte";
    import raum_default from '$lib/assets/raum_default.png'

	let loaded = $state(false);
    let facts = $state([
        {
            "title":"loading...",
            "description":"loading...",
            "icon":"",
            "id":0
        }
    ]);
    let cidx = $state(0);
    let nFacts = $state(0);
    let seen = $state(new Set([cidx]));

    let title = $derived(facts[cidx].title);
    let desc = $derived(facts[cidx].description);
    let icon = $derived(facts[cidx].icon);

    onMount (function() {
        fetch(`${base}/facts.json`)
        .then(response => response.json())
        .then(data => {
            facts = data;
            loaded = true;
            nFacts = facts.length;
        })
        newDeg();
    });

    let clicks = $state(0);

    let unlocked = $state(false);
    //if (sessionStorage.getItem('unlocked')) unlocked = JSON.parse(sessionStorage.getItem('unlocked'));
    function unlock() {
        unlocked = true;
        //sessionStorage.setItem('unlocked', JSON.stringify(true));
    }

    function prevFact() {
        newDeg();
        if (cidx > 0) cidx--;
        else cidx = nFacts-1;
        seen.add(cidx);
        if (seen.size == nFacts) unlock();
    }

    function nextFact() {
        newDeg();
        if (cidx >= nFacts-1)  cidx = 0;
        else cidx++;
        seen.add(cidx);
        if (seen.size == nFacts) unlock();
    }

    function newDeg() {
        var icon = document.querySelector('#fact-icon');
        var sign = Math.random() < 0.5 ? -1 : 1;
        icon.style.setProperty('--degrees', sign*Math.floor(Math.random()*12+5)+'deg');
    }

    $effect(()=>{
        if (clicks !== 0 && clicks % 4 == 0) {
            var icon_egg = document.getElementById('icon-egg');
            icon_egg.classList.add('jump-up');
        }
    })
</script>

<style>
    #facts-carousel {
        overflow: hidden;
        position: relative;
    }
    #fact-icon {
        --degrees: 10deg;
        transition: 140ms ease;
    }
    #fact-icon:hover {
        transform: rotate(var(--degrees));
    }
    #icon-egg {
        position: absolute;
        top: 100%;
        left: 50%;
        transform: translateX(-50%);
    }
    :global(.jump-up) {
        animation: jump-up 1000ms cubic-bezier(0.47, 0, 0.745, 0.715) forwards;
    }
    @keyframes jump-up {
        70% {
            top: 0;
        }
        100% {
            top: 100%;
        }
    }
</style>

<svelte:head>
    <title>Amur Leopard | The Zoo</title>
</svelte:head>

<Zoo/>
<Header/>
<div class="main-wrapper">
    <!-- facts panel -->
     <div id="facts-carousel" class="flex flex-col h-[60vh] min-h-[600px] w-screen max-w-screen mt-10">
        <div id="fact-container" class="flex flex-col flex-1 justify-start items-center p-10">
            <div title="view all facts to meet a leopard!" id="fact-counter" class="text-center">{cidx+1}/{nFacts}</div>
            <div onclick={clicks++} id="fact-icon" class="object-fit text-[8rem] min-h-1/3 h-1/3 max-h-1/3 w-auto place-content-center text-center m-5 text-[var(--cmain)]">{@html icon}</div>
            <div id="fact-title" class="text-[2.4rem] public-sans-bold">{@html title}</div>
            <div id="fact-desc">{@html desc}</div>
        </div>
        <div class="flex flex-row align-center justify-center gap-15 text-center">
            <button id="prev" class="facts-button" onclick={prevFact}>prev</button>
            <button id="next" class="facts-button" onclick={nextFact}>next</button>
        </div>
        <img src={raum_default} alt="Raum" id="icon-egg">
    </div>
    {#if unlocked}<MeetTab/>{/if}
</div>
<Footer {unlocked}/>