<script>
    export let searchTerm;
</script>
<!-- <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"> -->

<!-- <div class="ml-10 ...">
<form class="example" on:submit|preventDefault>
  <input type="text" 
        placeholder="Search for an event" 
        name="search"
        bind:value={searchTerm}>
  <button type="submit">Search</button>
</form>
</div> -->

<div class="flex justify-center items-center">
<form class="w-full max-w-sm" on:submit|preventDefault>
  <div class="flex items-center border-b border-teal-500 py-2">
    <input class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" 
    type="text" 
        placeholder="Search for an event" 
        name="search"
        bind:value={searchTerm}>
    <button class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" 
    type="submit">
      Search
    </button>
  </div>
</form>
</div>

<style>
    * {
  box-sizing: border-box;
}

form.example input[type=text] {
  padding: 9px;
  font-size: 17px;
  border: 1px solid grey;
  float: left;
  width: 40%; 
  /* 80% */
  background: #f1f1f1;
}


form.example button {
  float: left;
  width: 20%;
  padding: 9px;
  background:  #aaa;
  color: white;
  font-size: 17px;
  border: 1px solid grey;
  border-left: none; 
  cursor: pointer;
}

form.example button:hover {
  background: #3a3c3e;
}

form.example::after {
  content: "";
  clear: both;
  display: table;
}
</style>