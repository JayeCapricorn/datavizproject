<script>
    export let date;
    export let name;
    export let isLeft = true;
    export let eventID;
    import Tooltip from './Tooltip.svelte';
</script>

<!-- <Tooltip title="in {date} there were {name}">
	<div class="container"
    class:left={isLeft}
    class:right={!isLeft}
    id={eventID}>
    <div class="content">
      <h2>{date}</h2>
      <p>{name}</p>
    </div>
  </div>
</Tooltip> -->

<div class="container"
    class:left={isLeft}
    class:right={!isLeft}
    id={eventID}>
    <div class="content">
      <h2>{date}</h2>
      <p>{name}</p>
    </div>
  </div>

<!-- <div id={eventID}>
    <div class="absolute w-3 h-3 bg-gray-200 rounded-full mt-1.5 -left-1.5 border border-white dark:border-gray-900 dark:bg-gray-700"></div>
    <time class="mb-1 text-sm font-normal leading-none text-gray-400 dark:text-gray-500">{date}</time>
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white">{name}</h3>
</div> -->

<style>
/* Container around content */
.container {
  padding: 10px 40px;
  position: relative;
  background-color: inherit;
  width: 50%;
}

/* The circles on the timeline */
.container::after {
  content: '';
  position: center; 
  /* absolute */
  width: 25px;
  height: 25px;
  right: -17px;
  background-color: white;
  border: 4px solid #FF9F55;
  top: 15px;
  border-radius: 50%;
  z-index: 1;
}

/* Place the container to the left */
.left {
  left: 0;
}

/* Place the container to the right */
.right {
  left: 50%;
}

/* Add arrows to the left container (pointing right) */
.left::before {
  content: " ";
  height: 0;
  position: absolute;
  top: 22px;
  width: 0;
  z-index: 1;
  right: 30px;
  border: medium solid white;
  border-width: 10px 0 10px 10px;
  border-color: transparent transparent transparent white;
}

/* Add arrows to the right container (pointing left) */
.right::before {
  content: " ";
  height: 0;
  position: absolute;
  top: 22px;
  width: 0;
  z-index: 1;
  left: 30px;
  border: medium solid white;
  border-width: 10px 10px 10px 0;
  border-color: transparent white transparent transparent;
}

/* Fix the circle for containers on the right side */
.right::after {
  left: -16px;
}

/* The actual content */
.content {
  padding: 20px 30px;
  background-color: white;
  position: relative;
  border-radius: 6px;
}
</style>