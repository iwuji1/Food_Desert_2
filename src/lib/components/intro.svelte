<script>
    import {gsap} from 'gsap';

    import { onMount } from 'svelte';

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);

        let tl = gsap.timeline({
            scrollTrigger:{
                trigger: ".intro",
                start: "top 10%",
                end: "bottom 60%",
                scrub: 1,
                pin: true,
                toggleActions: "restart none none reverse"
            }
        })
        .from(".desert", {
            y: 50,
            opacity: 0,
            duration: 1
        },0)

    })

</script>

<style>

    .intro {
        font-family: sans-serif;
        display: flex;
        flex-direction: row;
        width: 100vw;
        z-index: 5;
        align-items: center;
    }

    .intro-left {
        width: 50%;
        display: flex;
        align-items: left;
        justify-content: center;
        flex-direction: column;
        padding: 5%;
        z-index: 6;
    }

    .intro-right {
        width: 50%;
        display: flex;
        flex-direction: column;
        z-index: 6;
    }

    .spacer {
      width: 100vw;
      height: 100vh;
      background-repeat: no-repeat;
      background-position: center;
      background-size: cover;
      z-index: 2;
      position: absolute;
    }

    .desert {
      background-image: url('/backgrounds/Desert_BG.svg');
    }

</style>

<div class="intro">
    <div class="intro-left">
        <h1> What Is A Food Desert?</h1>
        <p> Food deserts can be described as geographic areas where residents’ access to affordable, healthy food options (especially fresh fruits and vegetables) is restricted or nonexistent due to the absence of grocery stores within convenient traveling distance.</p>
    </div>
    <div class="intro-right">
        <p>This is the other side</p>

    </div>
    <div class="spacer desert"></div>
</div>