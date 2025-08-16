<script>
    import Zoo from "$lib/zoo.svelte";
    import Footer from "$lib/footer.svelte";
</script>

<style>
    .wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-self: center;
        padding-bottom: 10vh;
    }
    #opener {
        font-size: 3.2rem;
        max-width: 75ch;
        margin: 0 2em;
        text-align: center;
    }
    #subtitle {
        max-width: 75ch;
        padding: 0 10px;
    }

    section {
        max-width: 1500px;
    }

    div.back-forth {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        width: 90vw;
        max-width: 100%;
        padding: 5px 10px;
        gap: 1em;
        margin: 2em 0;
    }

    .back-forth > * {
        position: relative;
        border-radius: 0.6em;
        padding: 10px;
        max-width: 75ch;
    }
    .back-forth >:nth-child(odd) {
        align-self: start;
        margin-left: 1.344em;
        background-color: var(--cneutral);
        &::after {
            content: '';
            position: absolute;
            left: 0;
            top: 50%;
            width: 0;
            height: 0;
            border: 1.344em solid transparent;
            border-right-color: var(--cneutral);
            border-left: 0;
            border-bottom: 0;
            margin-top: -0.672em;
            margin-left: -1.344em;
        }
    }
    .back-forth >:nth-child(even) {
        align-self: end;
        margin-right: 1.344em;
        background-color: var(--camain);
        &::after {
            content: '';
            position: absolute;
            right: 0;
            top: 50%;
            width: 0;
            height: 0;
            border: 1.344em solid transparent;
            border-left-color: var(--camain);
            border-right: 0;
            border-bottom: 0;
            margin-top: -0.672em;
            margin-right: -1.344em;
        }
    }

    h1 {
        text-align: left;
        font-family: 'Bokor';
        font-size: 3rem;
    }

    .important {
        color: var(--crit);
        font-weight: bold;
    }

    .cartoon {
        display: grid;
        width: 90vw;
        max-width: 100%;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        grid-template-rows: 200px;
        grid-auto-rows: 200px;
        font-family: 'Comic Relief', 'Courier New', Courier, monospace;
        font-size: 1.4rem;
    }

    .cartoon a {
        color: var(--cmain);
    }
    .cartoon > div {
        width: 100%;
        height: 100%;
        border: 8px solid var(--ctheme);
        border-top-left-radius: 255px 15px; /** from https://codemyui.com/hand-drawn-border-buttons-css/ */
        border-top-right-radius: 15px 225px;
        border-bottom-right-radius: 225px 15px;
        border-bottom-left-radius:15px 255px;
        padding: 0.8em;
        overflow: auto;
    }

    @media screen and (min-width: 740px) {
        .wrapper {
            padding-top: 20px;
        }
        #opener {
            font-size: 5.2rem;
            max-width: 75ch;
        }
        h1 {
            font-size: 5rem;
        }
        .cartoon {
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            grid-template-rows: 300px;
            grid-auto-rows: 300px;
            font-size: 2rem;
        }
    }

    @media only screen and (min-width: 1000px) {
        

        
    }
</style>

<svelte:head>
    <title>Extinction Status | Amur Leopard | The Zoo</title>
</svelte:head>

<Zoo/>
<div class="wrapper">
    <div id="opener" class="public-sans-bold">
        Amur leopards are <span class="critical">Critically Endangered</span>
    </div>
    <h3 id="subtitle" class="text-center">
        In the late 1970s, the Amur leopard dropped to just 30 individuals in the wild.<br/>
        The population has only grown to around 100 since then.<br/>
        <p class="text-[1rem]">THIS WEBSITE IS NOT ASSOCIATED WITH ANY EXTERNAL WEBSITE OR INITIATIVE.</p>
    </h3>
    
    <section id="history-wrapper">
        <div class="back-forth">
            <p>How did it come to this point?</p>
            <p>That's a great question! Well, it all started when the Roman Empire was founded....</p>
        </div>
        <h1>History</h1>
        <div class="cartoon grid gap-5">
            <div>Historical records indicate that Amur leopards have lived throughout eastern Siberia, northeastern China, the mountains to Beijing's northwest, Manchuria, and the Korean Peninsula.</div>
            <div>They were ruthlessly hunted in the Koreas for their skins. At least 624 were killed between 1910 and 1945 during Japanese Rule. The last known South Korean leopard was captured in 1970.</div>
            <div>In Russia, the leopard's native range has <span class="important">decreased by 80%</span>. In China, their range shrank from covering the Lesser Khingan, Changbai, and Wanda Mountains to a nearly only isolated areas in Jilin province.</div>
        </div>
    </section>
    
    <section id="threats-wrapper">
        <div class="back-forth">
            <p>Thanks for the history, but what I really meant was what caused the decline of the Amur leopard population?</p>
            <p>Oho, I was just getting to that part! You see, after the Romans found Atlantis, they...</p>
        </div>
        <h1>Threats</h1>
        <div class="cartoon grid gap-5">
            <div>Amur leopards' forest habitats are accessible to poachers due to the surrounding agriculture and villages. Not only do the poachers hunt the Amur leopard for their spotted fur, but important prey species as well.</div>
            <div>This creates a problem known as <span class="important">prey scarcity</span>; as a result of excessive poaching and hunting, the prey base in otherwise habitable areas cannot sustain large populations of leopards and similar predators.</div>
            <div>The underlying problem is <span class="important">illegal wildlife trade</span>. Amur leopards have historically been poached nearly to the point of no return. Their numbers may have recovered since then but their native habitat cannot currently support them.</div>
        </div>
    </section>
    
    <section id="conservation-wrapper">
        <div class="back-forth">
            <p>... How are we ever gonna remedy this disaster?!</p>
            <p>Wow, another great question! Well, as it turns out, us Amur leopards are basically invincible and....</p>
        </div>
        <h1>Conservation Efforts</h1>
        <div class="cartoon grid gap-5">
            <div>Amur leopards are an apex predator of their ecosystem which means they regulate the populations of prey species, which in turn maintains the natural flora. Conservation of their habitat benefits other species like Amur tigers and native prey populations.</div>
            <div>The solution to revitalizing the Amur leopard subspecies begins with <span class="important">allowing the prey populations to recover</span>. The leopards can only return to their home along the Russia-China border when there are habitats that can sustain the leopard populations.</div>
            <div>Conservation efforts include Land of the Leopard National Park in Russia, anti-poaching initiatives in their habitat, programs to stop the illegal trade in leopard parts, limits on poaching of prey species, and reintroduction of prey species to rebuild prey populations.</div>
            <div>Do you want to be a part of this journey? You can! Prevent poaching by <a href="https://protect.worldwildlife.org/page/53484/petition/1" target="_blank" rel="noopener noreferrer">stopping wildlife crime</a>, support current leopard populations by <a href="https://gifts.worldwildlife.org/gift-center/gifts/Species-Adoptions/Amur-Leopard?" target="_blank" rel="noopener noreferrer">adopting an Amur leopard</a>, or support Amur leopard conservation initiatives by volunteering or donating.</div>
            <div><q>With the right conservation efforts, we can bring them back and ensure long-term conservation of the region.</q> <cite>&mdash;WWF</cite></div>
        </div>
    </section>
</div>
<!-- raum chibis, maybe a cartoon? -->
<div id="back">
    <a class="text-[2.4rem]" href="./" aria-label="Go Home"><i class="fa-solid fa-arrow-left"></i></a>
</div>
<Footer/>