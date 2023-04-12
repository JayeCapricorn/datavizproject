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
    <ul class="flex">
        <li class="mr-6">
          <a class="text-gray-500 hover:text-blue-800" href="/frontpage">Frontpage</a>
        </li>
        <li class="mr-6">
          <a class="text-gray-500 hover:text-blue-800" href="/">Timeline</a>
        </li>
    </ul>
</main>

<svelte:head>
	<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet"/>
</svelte:head>

<style>
    main {
       text-align: center;
       font-family: "Nunito", sans-serif;
       font-weight: 300;
       line-height: 2;
       font-size: 24px;
       color: var(--color-text);
       margin-top: 10px;
       margin-left: 100px;
   }

   li {
    display: inline;
  }
</style>