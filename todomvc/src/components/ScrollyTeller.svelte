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
  <div
    class="background"
    slot="background"
    bind:clientWidth={width}
    bind:clientHeight={height}
  >
    <BackgroundImg {index} />
  </div>

  <div class="foreground" slot="foreground">
    <section>
      <h4>Influence of Natural Hazard</h4>
      <p>
        Natural disasters have caused thousands of deaths per year in Central
        American countries.
      </p>
      <!-- <img src="/images/test3.png" style="width: 60%"/> -->
    </section>

    <section>
      <h4>Direct Relationship between Disasters and Migration intention</h4>
      <!-- <img src="/images/netmigration.png" style="width: 60%"/> -->
      The number of disasters has a positive correlation with Central American net
      migration.
      <!-- <img src="/images/test5.PNG" style="width: 60%"/> -->
    </section>
    <section>
      <h4>Intermediate Variable - Economy</h4>
      At the same time, natural disasters have resulted in significant economic damages.
      <!-- <img src="/images/test4.png" style="width: 60%"/> -->
      Disasters affect economic variables such as the consumer and wholesale price
      index.
      <!-- <img src="/images/test6.png" style="width: 90%"/>
      <img src="/images/test8.PNG" style="width:550px"/> -->
    </section>
    <!-- <section> Migration rates in Central America have peaked in certain years such as 1980.
      <img src="/images/test2.PNG" style="width: 50%"/>
    </section> -->
    <!--      <section style="width: 600px; position: relative;
      left: 500px;">
      <img src="/images/test8.PNG"/> -->
    <!--     </section> -->
    <section>
      <h4>Intermediate Variable - Food Security</h4>
      Disasters also worsen food insecurity for residents.
      <!-- <img src="/images/test7.PNG" style="width: 60%"/>
      <img src="/images/test9.PNG" style="width:550px"/> -->
    </section>
    <section>
      <h4>LA LA LA</h4>
      lalalalalalala
    </section>
    <section>
      <h4>LA LA LA</h4>
      lalalalalalala
    </section>
    <section>
      <h4>LA LA LA</h4>
      lalalalalalala
    </section>
    <section>
      <h4>LA LA LA</h4>
      lalalalalalala
    </section>
  </div>
</Scroller>

<p> This data visualization was made with data contributed by the United Nations World Food Programme (WFP).
</p>

<style>
  p {
    font: 20px sans-serif;
    font-family: "Nunito", sans-serif;
    text-align: center;
  }
    /* .img2 {
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
        margin-top: 20px;
        margin-bottom: 20px;
        margin-left: auto;
        margin-right: auto;
        width: 100%;
    } */
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
    position: relative;
    left: 500px;
    height: 90vh;
    background-color: rgba(255, 255, 255, 0.2); /* 20% opaque */
    color: white;
    /*       outline: rgb(77, 77, 77) solid 1px; */
    text-align: center;
    width: 600px;
    /* max-width: 750px;  */
    color: black;
    padding: 1em;
    margin: 0 0 2em 0;
  }
</style>
