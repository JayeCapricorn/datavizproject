<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import BackgroundImg from "./BackgroundImg.svelte";

  let count, index, offset, progress;
  let width, height;
</script>

<div>
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
    <section style="padding-top: 50%;">
      In Honduras, Guatemala, and El Salvador, natural disasters each year cause
      thousands of death, tens of thousands of people becoming homeless, and
      generally affecting millions of people. Among its many other devastating
      effects, in this study, we investigate the impact it has on the migration
      behavior in these three countries.
    </section>
    <section>
      Historically, tens of thousdans of peoplpe in these countries emigrate to
      other countries. We find that the peaks in this emigration tendency
      usually correlates with significant natural disasters. For example, xxxxxx
    </section>
    <section>
      Indeed, we find a strong correlation between the frequency of natural
      disasters and the number of emigrants in each year in these three
      countries. But this correlation is only the strongest when we consider the
      emigration <b>three</b> years after the disaster, showing a delayed effect
      of disasters (R^2=0.32, p=1.6 * 10^-3). This three-year window is a recurring
      theme in our analysis and will appear below too.
    </section>
    <section>
      Nevertheless, directly analyzing the relationship between disaster
      frequency and migration behvaior is noisy, as it is mediated by many other
      variables. We take inspiration from the responses to the question "How has
      the situation of COVID-19 and / or natural hazards impacted your life and
      that of your home?" from the World Food Programme's survey. A very common
      theme in the responpses relates to the economy and employment, and thus we
      study how it could be affected by natural disasters and in turn affect
      emigration.
    </section>
    <section>
      In general, natural disasters result in hundreds of millions of economic
      damage each year in these countries. Taking a more microscopic look, we
      can see that borrowing from commercial banks usually surges in the same
      year as the disaster happens (R^2=0.73, p=8.4 * 10^-6), and three years
      later, we observe an increase in the wholesale price index (R^2=0.86,
      p=6.9 * 10^-17) and the consumer price index (R^2=0.83, p=1.5 * 10^-46)
      (TODO: what are these?).
    </section>
    <section>
      This economic impact, in turn, affects the emigration behavior. For
      example, the wholesale price index strongly correlates with the number of
      emigrants in a year (R^2=0.86, p=3.6 * 10^-6). We also use the World Food
      Programme data for an individual-level analysis. Inspecting the features
      with the largest magnitude from a ridge regression analysis, we find that
      the respondants' intention to emigrate outside their countries is strongly
      affected by their indebtedness and inversely affected by their
      expenditure.
    </section>
    <section>
      Stepping back to what respondants to the survey perceive as the main
      impact of natural disasters, we find food as another commong theme. Hence,
      we now turn to studying how food insecurity could act as a mediator
      between natural disasters and emigration.
    </section>
    <section>
      As before, three years after a natural disaster, we find a substantial
      increase in the prevalance of food insecurity in these populations, up to
      20% when there are 5 disasters in a year (R^2=0.88, p=1.5 * 10^-6).
    </section>
    <section>
      And in turn, while food insecurity does not strongly affect emigration
      intention, we discover that they drive people to internally migrate to
      other parts of their countries. Among the top factors that contribute to
      people's intention to internally migrate, we find many that are related to
      food insecurity.
    </section>
    <section>
      And in turn, while food insecurity does not strongly affect emigration
      intention, we discover that they drive people to internally migrate to
      other parts of their countries. Among the top factors that contribute to
      people's intention to internally migrate, we find many that are related to
      food insecurity.
    </section>
    <section>
      And in turn, while food insecurity does not strongly affect emigration
      intention, we discover that they drive people to internally migrate to
      other parts of their countries. Among the top factors that contribute to
      people's intention to internally migrate, we find many that are related to
      food insecurity.
    </section>
    
  </div>
  
</Scroller>
</div>

<p >
  This data visualization was made with data contributed by the United Nations
  World Food Programme (WFP).
</p>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap");
  
  p {
    z-index: 10;
    position: relative;
    background: #efe9dd;
    margin: 0;
    padding: 10px;
    font: 10px sans-serif;
    font-family: "Nunito", sans-serif;
    text-align: center;
  }
  .background {
    width: 55%;
    height: 100vh;
    position: fixed;
    left: 2%;
    top: 0;
    /* outline: green solid 3px; */
    text-align: center;

  }

  .foreground {
    width: 35%;
    height: auto;
    position: relative;
    left: 60%;
    /* outline: red solid 3px; */
  }

  section {
    font-size: 14px ;
    font-family: 'Open Sans', sans-serif;
    position: relative;
    height: 90vh;
    background-color: rgba(255, 255, 255, 0); /* 20% opaque */
    text-align: justify;
    width: 100%;
    color: black;
    /* padding:  0; */
    margin: 0 0 2em 0x;
  }

  div{
    /* background-color:#efe9dd; */
  }

</style>
