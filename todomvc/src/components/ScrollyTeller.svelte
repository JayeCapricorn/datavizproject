<script>
    import Scroller from "@sveltejs/svelte-scroller";
    import BackgroundImg from "./BackgroundImg.svelte";
  
    let count, index, offset, progress;
    let width, height;
</script>

<Scroller
  top={0.0}
  bottom={0.9}
  threshold={0.5}
  bind:count
  bind:index
  bind:offset
  bind:progress
>
  <div class="background" slot="background"
  bind:clientWidth={width}
    bind:clientHeight={height}>
    <BackgroundImg {index}/>
  </div>

  <div class="foreground" slot="foreground" >
    <section> Migration rates in Central America have changed and peaked in certain years.
      <img src="/images/test2.PNG" style="width: 50%"/>
    </section>
    <section>Natural disasters have caused thousands of deaths per year in Central American countries. 
      <img src="/images/test3.png" style="width: 50%"/>
    </section>
    <section> At the same time, natural disasters have resulted in significant economic damages. 
      <img src="/images/test4.png" style="width: 50%"/>
    </section>
    <section>
      <!-- <img src="/images/image.png" class="img2"/>
        <img src="/images/imgtest.PNG" class="img3"/> -->
    </section>
    <section> </section>
  </div>

</Scroller>

<style>
    .img2 {
        position: relative; 
        right: 120px;
        width: 30%
    }
    .img3 {
        position: relative; 
        right: 20px;
        top: 80px;
        width: 30%
    }
    img {
        display: block;
        margin-left: auto;
        margin-right: auto;
        width: 100%;
    }
    .background {
      width: 100%;
      height: 100vh;
      position: relative;
      /* outline: green solid 3px; */
    }
  
    .foreground {
      width: 50%;
      margin: 0 auto;
      height: auto;
      position: relative;
      /* outline: red solid 3px; */
    }

    section {
      font: 20px sans-serif;
      font-family: "Nunito", sans-serif;
      /* position: relative; 
      left: 300px; */
      height: 80vh;
      background-color: rgba(255, 255, 255, 0.2); /* 20% opaque */
      color: white;
      /* outline: magenta solid 3px; */
      text-align: center;
      /* width: 400px;   */
      max-width: 750px; 
      color: black;
      padding: 1em;
      margin: 0 0 2em 0;
    }
  </style>
  