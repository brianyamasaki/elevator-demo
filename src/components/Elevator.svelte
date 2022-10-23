<div class="elevator" bind:clientWidth="{elementWidth}" bind:this="{doorBackground}">
  <div class="left-door" style:right={open ? `${elementWidth}px` : `${elementWidth / 2}px`}></div>
  <div class="right-door" style:left={open ? `${elementWidth}px` : `${elementWidth / 2}px`}></div>
</div>

<script>
  import { onMount } from 'svelte';

  const floors = [
    {
      floor: 1,
      img: '/assets/grocery-level.jpg'
    },
    {
      floor: 2,
      img: '/assets/mall-level.jpg'
    },
    {
      floor: 3,
      img: '/assets/mens-clothing.jpg'
    },
    {
      floor: 4,
      img: '/assets/womens-clothing.jpg'
    }
  ];

  let iFloor = 0;

  const nextFloor = () => {
    iFloor = (iFloor + 1) % floors.length;
  }

  let open;
  let elementWidth;
  let doorBackground;
  onMount(() => {
    open = false;
    setInterval(() => {
      open = !open;
      if (!open) {
        nextFloor();
        doorBackground.style.backgroundImage = `url(${floors[iFloor].img})`;  
      }
    }, 5000)
  });

</script>
<style>
  .elevator {
    height: 400px;
    background: url('/assets/grocery-level.jpg');
    background-size: 100%;
    position:relative;
  }

  .left-door {
    position:absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    transition: 1s;
    background-color: red;
  }
  .right-door {
    position:absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 50%;
    transition: 1s;
    background-color: blue;
  }
</style>