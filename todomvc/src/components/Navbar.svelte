<!-- <script>

</script>

<div class="container-fluid">
  <nav class="navbar navbar-inverse navbar-default" >
   <div class="container-fluid">

       <ul class="nav navbar-nav navbar-right">
         <li><a href="/frontpage">Frontpage</a></li>
         <li><a href="/">Timeline</a></li>
       </ul>
     </div>
   </div>

<style>

</style> -->
<script>

</script>

<main>
    <ul>
        <li>
          <a href="/frontpage">Frontpage</a>
        </li>
        <li>
          <a href="/">Timeline</a>
        </li>
        <li>
          <a href="/frontpage">Maps</a>
        </li>
        <li>
          <a href="/frontpage">Analysis</a>
        </li>
    </ul>
</main>

<!-- <svelte:head>
	<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet"/>
</svelte:head> -->

<style>
  @import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap");
    :root {
        --color-bg: #ffffff;
        --color-outline: #c2c2c2;
        --color-shadow: hsl(0, 0%, 0%, 0.1);
        --color-text: #3f4252;
        --color-bg-1: hsla(0, 0%, 0%, 0.2);
        --color-shadow-1: hsl(0, 0%, 96%);
    }
    *,
    *::before,
    *::after {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    a:visited { 
      text-decoration: none; 
      color: grey; 
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

    main {
       text-align: left;
       font-family: "Nunito", sans-serif;
       font-weight: 300;
       line-height: 2;
       font-size: 15px;
       color: var(--color-text);
       margin-top: 10px;
       margin-left: 100px;
   }

   li {
    display: inline;
  }
</style>