<script>
  import { Canvas } from '@threlte/core'
  import Scene from '$lib/components/scene.svelte'
  import Intro from '$lib/components/intro.svelte'
</script>
<style>
    :global(html) {
        scroll-behavior: smooth;
    }
    
    :global(body) {
    margin: 0;
    overflow-x: hidden;
    background: #FFE135;
    background: radial-gradient(circle,rgba(255, 225, 53, 1) 0%, rgba(255, 200, 0, 1) 100%);
}

  .Hero {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .Hero_text {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    text-align: center;
    color: white;
    z-index: 1;
    flex-direction: column;
    gap: 20px;
  }

  .Hero_text p {
    font-size: 1.5rem;
    margin: 0;
    color: #016f08;
    font-family: sans-serif;
    font-weight: 900;
    text-transform: uppercase;
  }

  .Hero_text h1 {
    font-size: 2.5rem;
    margin: 0;
    color: #6b3e26;
    font-family: sans-serif;
    width: 50%;
    
  }

  .scroll-icon a {
  display: inline-block;
  -webkit-transform: translate(0, 70%);
  transform: translate(0, 70%);
  color: #016f08;
  font : normal 400 20px/1 'Josefin Sans', sans-serif;
  letter-spacing: .1em;
  text-decoration: none;
  transition: opacity .3s;
}
.scroll-icon a:hover {
  opacity: .5;
}
  
  #section07 a {
    padding-top: 100px;
}

#section07 a span {
    position: absolute;
    top: 0;
    left: 50%;
    width: 24px;
    height: 24px;
    margin-left: -12px;
    border-left: 1px solid #016f08;
    border-bottom: 1px solid #016f08;
    -webkit-transform: rotate(-45deg);
    transform: rotate(-45deg);
    -webkit-animation: sdb07 2s infinite;
    animation: sdb07 2s infinite;
    opacity: 0;
    box-sizing: border-box;
    }
    #section07 a span:nth-of-type(1) {
    -webkit-animation-delay: 0s;
    animation-delay: 0s;
    }
    #section07 a span:nth-of-type(2) {
    top: 16px;
    -webkit-animation-delay: .15s;
    animation-delay: .15s;
    }
    #section07 a span:nth-of-type(3) {
    top: 32px;
    -webkit-animation-delay: .3s;
    animation-delay: .3s;
    }
    @-webkit-keyframes sdb07 {
    0% {
        opacity: 0;
    }
    50% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
    }
    @keyframes sdb07 {
    0% {
        opacity: 0;
    }
    50% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
    }

    .spacer {
      width: 100%;
      height: 100%;
      background-repeat: no-repeat;
      background-position: center;
      background-size: cover;
      z-index: 2;
      position: absolute;
    }

    .layer1 {
      background-image: url('/backgrounds/Bottom-waves.svg');
    }

    .intro {
        display: flex;
        height: 100vh;
        width: 100vw;
        justify-content: center;
        align-items: flex-end;
        flex-direction: row;
        gap: 20px;
    }
</style>
<svelte:head>
    <title>Food Desert</title>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/gsap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/ScrollTrigger.min.js"></script>
</svelte:head>

<div class="Hero" id="Hero">
    <div class="Hero_text">
        <p>Food Deserts</p>
        <h1>Over a million people live in places where it's easier to buy crisps than fresh fruit</h1>

        <section id="section07" class="scroll-icon">
            <a href="#Intro">
                <span></span>
                <span></span>
                <span></span>
                _
            </a>
        </section>
    </div>
    <Canvas>
    <Scene />
    </Canvas>
</div>
<div class="spacer layer1"></div>

<div class="intro" id="Intro">
  <Intro />  
</div>