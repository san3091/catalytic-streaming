<script>
  import { tweened } from 'svelte/motion'
  import { cubicInOut } from 'svelte/easing'
  import CarouselItem from './CarouselItem/CarouselItem.svelte'

  export let albums
  export let selectAlbum
  let carouselWidth, itemsWidth
  let carouselOffset = tweened(0, { easing: cubicInOut })
  $: slideDistance = (Math.floor(carouselWidth / 190) - 1) * 190
  $: overflowWidth = itemsWidth - carouselWidth

  const slideLeft = () => {
    const nextOffset = $carouselOffset - slideDistance

    nextOffset > 0
      ? carouselOffset.set(nextOffset)
      : carouselOffset.set(0)
  }

  const slideRight = () => {
    const nextOffset = $carouselOffset + slideDistance

    overflowWidth < nextOffset
      ? carouselOffset.set(overflowWidth)
      : carouselOffset.set(nextOffset)
  }
</script>

<h4>Current Selections</h4>
<div 
  class='album-carousel'
  bind:clientWidth={carouselWidth}>
  {#if $carouselOffset}
    <button 
      class='previous-button'
      on:click={slideLeft}
    >left
    </button>
  {/if}
  <div 
    class='carousel-items' 
    style='--carousel-offset:{$carouselOffset}px'
    bind:clientWidth={itemsWidth}
  >
    {#each albums as album}
      <CarouselItem album={album} selectAlbum={selectAlbum} />
    {/each}
  </div>
  {#if $carouselOffset != overflowWidth }
    <button 
      class='next-button'
      on:click={slideRight}
    >right
    </button>
  {/if}
</div>

<style>
  .album-carousel {
    position: relative;
    display: flex;
    overflow: hidden;
    margin-bottom: 10px;
  }

  .carousel-items {
    position: relative;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    position: relative;
    background-color: aliceblue;
    right: var(--carousel-offset);
  }
  
  button {
    height: 100%;
    opacity: 0.5;
    position: absolute;
    width: 80px;
    z-index: 1;
  }

  .previous-button{
    left: 0;
  }

  .next-button {
    right: 0;
  }
</style>