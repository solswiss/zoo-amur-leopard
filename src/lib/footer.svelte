<script>
    export let unlocked;
</script>

<div id="footer" class="grid grid-cols-3 grid-rows-1 place-content-center px-10 pt-10 pb-60">
    <div class="flex flex-col">
        <div class="title public-sans-bold">Pages</div>
        <a href="./" aria-label="Go Home">home</a>
        <a href="./critical" aria-label="Go To Endangered Status Info Page">endangered</a>
        {#if unlocked} <a href="./meet-raum" aria-label="Go Meet Raum">raum</a>{/if}
    </div>
    <div class="flex flex-col">
        <div class="title public-sans-bold">Further Reading</div>
        <a href="https://www.worldwildlife.org/media?species_id=amur-leopard" target="_blank" rel="noopener noreferrer" aria-label="Go To WWF Website On Amur Leopards">WWF</a>
        <a href="https://www.ifaw.org/animals/amur-leopard" target="_blank" rel="noopener noreferrer" aria-label="Go To IFAW Website On Amur Leopards">IFAW</a>
        <a href="https://en.wikipedia.org/wiki/Amur_leopard" target="_blank" rel="noopener noreferrer" aria-label="Go To Amur Leopard Wikipedia Article">Wikipedia</a>
    </div>
    <div class="flex flex-col">
        <div class="title public-sans-bold">Meta</div>
        <span>Made by <a href="http://github.com/solswiss" target="_blank" rel="noopener noreferrer" aria-label="Go To The Maker's Github">Swiss</a></span>
        <span>Made for <a href="http://zoo.hackclub.com" target="_blank" rel="noopener noreferrer">Zoo</a> of <a href="http://hackclub.com" target="_blank" rel="noopener noreferrer">Hackclub</a></span>
    </div>
</div>