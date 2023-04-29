<script>
    export let index;

    let isVisible;
    let imgurl = "/images/bgimage.PNG";
    // let imgurl = "/src/assets/bgimage.PNG";
    // let testurls = {0: "/src/assets/test.PNG", 
    //                 1: "/src/assets/economic.PNG", 
    //                 2: "/src/assets/people.PNG", 3: "/src/assets/deaths.PNG"};

    $: if (index > 2) {
        isVisible = true;
    } else {
        isVisible = false;
    }
</script>

<main class:visible={isVisible}>
    <!-- <img src={testurls[index]} alt="background image" class="center"/> -->
    {#if index === 4}
    <img src="/images/image.png" class="img2"/>
    <img src="/images/imgtest.PNG" class="img3"/>
    <img src={imgurl} alt="background image" class="center"/>
    {:else}
    <img src={imgurl} alt="background image" class="center"/>
    {/if}
</main>

<style>
     .img2 {
        z-index: 3;
        position: absolute; 
        left: 150px;
        width: 20%
    }
    .img3 {
        z-index: 3;
        position: absolute; 
        right: 200px;
        top: 80px;
        width: 20%
    }

    .center {
        display: block;
        margin-left: auto;
        margin-right: auto;
        width: 80%;
        height: 90%;
        }
    main {
    /* width: 100%;
    height: 100vh;
    position: absolute; */
    opacity: 0;
    visibility: hidden;
  }

  main.visible {
    opacity: 1;
    visibility: visible;
  }

</style>