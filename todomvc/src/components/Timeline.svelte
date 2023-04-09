<script>
    import Scroll from "./Scrolly.svelte";
    import Search from './Search.svelte';
    import Event from './Event.svelte';
    export let testdates;

    let currentStep;
	let searchTerm;
	const getResults = () => {
		for (let evt of testdates) {
			if(evt.name.includes(searchTerm) || evt.date.toString().includes(searchTerm)) {
				return moveIntoView(evt.name);
			}
		}
	}

	const moveIntoView = (element) => {
		document.getElementById(element).scrollIntoView(
			{
				behavior: "smooth"
			}
		);
	}
</script>

<!-- <header>
	<Search bind:searchTerm 
	        on:submit={getResults}/>
</header> -->

<!-- <section>
	<Scroll bind:value={currentStep}>
		{#each testdates  as {name, date}, i}
			<div class="step" class:active={currentStep === i}>
				<div class="step-content">
					<Event {date} {name} eventID={name}/>
				</div>
			</div>
		{/each}
	</Scroll>
</section> -->

<main>
<div class="timeline">
	{#each  testdates  as {name, date}, i}
		<Event 
		{date} 
		{name}
		isLeft = {i%2 === 0}
		eventID={name}/>
	{/each}
  </div>
</main>


<!-- <ol class="relative border-l border-gray-200 dark:border-gray-700">                  
  {#each  testdates  as {name, date}, i}
  <li class="mb-10 ml-4">
    <Event 
		{date} 
		{name}
		isLeft = {i%2 === 0}
		eventID={name}/>
  </li>
	{/each}
</ol> -->


<style>
    	.step {
    height: 90vh;
    display: flex;
    place-items: center;
    justify-content: center;
  }

  .step-content {
    background: whitesmoke;
    color: #ccc;
    padding: .5rem 1rem;
    transition: background 500ms ease, color 500ms ease;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, .2);
  }

	.step.active .step-content {
		background: white;
		color: black;
	}

	/* Set a background color */
main {
  /* background-color: #474e5d; */
  font-family: Helvetica, sans-serif;
  margin-top: 90px;
  overflow: scroll;
}

/* The actual timeline (the vertical ruler) */
.timeline {
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
}

/* The actual timeline (the vertical ruler) */
.timeline::after {
  content: '';
  position: absolute;
  width: 6px;
  background-color: white;
  top: 0;
  bottom: 0;
  left: 50%;
  margin-left: -3px;
}

/* Media queries - Responsive timeline on screens less than 600px wide */
@media screen and (max-width: 600px) {
/* Place the timelime to the left */
  .timeline::after {
    left: 31px;
  }

/* Full-width containers */
  .container {
    width: 100%;
    padding-left: 70px;
    padding-right: 25px;
  }

/* Make sure that all arrows are pointing leftwards */
  .container::before {
    left: 60px;
    border: medium solid white;
    border-width: 10px 10px 10px 0;
    border-color: transparent white transparent transparent;
  }

/* Make sure all circles are at the same spot */
  .left::after, .right::after {
    left: 15px;
  }

/* Make all right containers behave like the left ones */
  .right {
    left: 0%;
  }
}
</style>