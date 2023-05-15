<script>
</script>

<main>
  <nav>
  <div class="navbar">
    <ul>
      <a href="/">FRONTPAGE</a>
      <a href="/timeline">TIMELINE</a>
    </ul>
  </div>
  <!-- <ul>
          <a href="/analysis">Analysis</a>
        </li>  -->
  <!-- </ul> -->
</nav>
</main>

<style>
  /* @import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap"); */

  @import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap");
  :root {
    --color-bg: #ffffff;
    /* --color-outline: #c2c2c2; */
    /* --color-shadow: hsl(0, 0%, 0%, 0.1); */
    --color-text: #949494;
    /* --color-bg-1: hsla(0, 0%, 0%, 0.2); */
    /* --color-shadow-1: hsl(0, 0%, 96%); */
  }
  *,
  *::before,
  *::after {
    /* margin: 4px; */
    padding: 0;
    box-sizing: border-box;
  }
  a:link{
    text-decoration: none;
  }

  a:visited {
    text-decoration: none;
    color: rgb(87, 87, 87);
  }

  .navbar a:hover{
    color:black
  }
  
  .navbar {
  background-color: rgba(255,255,255,0.4);
  overflow: hidden;
  padding:10px 25px;
  }

  .navbar ul{
    display:inline-block
  }
  /* main {
        height: 100%;
        display: grid;
        place-content: center;
        text-align: center;
        font-family: "Nunito", sans-serif;
        font-weight: 300;
        line-height: 2;
        font-size: 24px;
        color: var(--color-text);
    } */

  .navbar a {
    text-align: left;
    font-family: 'Open Sans', sans-serif;
    font-weight: 400;
    line-height: 1;
    font-size: 17px;
    color:grey;
    margin-left: 25px; 
  }

  main{
    z-index: 1;
  }

  /* li {
    display: inline;
  } */
</style>
