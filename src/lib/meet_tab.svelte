<style>
    #meet-container {
        background: url('https://images.squarespace-cdn.com/content/v1/67da3ab08606a379b294668d/63591dbd-0a58-470d-a23f-0e8f1ca8ea62/Chalu-Snow-Jasmine-Cloud.png') center / contain no-repeat;
        border-radius: 1em;
        align-items: center;
        transform: translateY(0);
        animation: float 1000ms ease-in-out infinite alternate;
    }
    i {
        animation: 1000ms nudge-right ease-in-out infinite alternate;
    }
    @keyframes nudge-right {
        to {
            transform: translateX(1rem);
        }
    }
    @keyframes float {
        to {
            transform: translateY(12px);
        }
    }
</style>
<div id="meet-container" class="mt-20 w-[90vw] max-w-[700px] h-[50vw] max-h-[300px] p-30 flex flex-col gap-2 mx-auto text-center">
    <a href="./meet-raum"><h1 class="public-sans-bold">Meet Raum! <i class="fa-solid fa-arrow-right"></i></h1></a>
    <h3>A virtual Amur leopard in its native habitat*</h3>
    <p class="text-[1.2rem]">*The author had not met an Amur leopard before making this.</p>
</div>