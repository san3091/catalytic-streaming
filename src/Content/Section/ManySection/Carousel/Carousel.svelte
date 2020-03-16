<script>
  import { tweened } from 'svelte/motion'
  import { cubicInOut } from 'svelte/easing'
  import { fade } from 'svelte/transition'
  import AlbumTile from '../../AlbumTile/AlbumTile.svelte'

  export let albums
  export let headerText
  export let selectAlbum
  export let selectedAlbum
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

<div class='carousel-container'>
  <h3>{headerText}</h3>
  <div 
    class='album-carousel'
    bind:clientWidth={carouselWidth}>
    {#if $carouselOffset}
      <button 
        class='previous-button'
        transition:fade
        on:click={slideLeft}
      >
        <i class="material-icons">keyboard_arrow_left</i>
      </button>
    {/if}
    <div 
      class='carousel-items' 
      style='--carousel-offset:{$carouselOffset}px'
      bind:clientWidth={itemsWidth}
    >
      {#each albums as album}
        <AlbumTile 
          album={album} 
          selectAlbum={selectAlbum}
          selected={selectedAlbum == album} />
      {/each}
    </div>
    {#if $carouselOffset != overflowWidth }
      <button 
        class='next-button'
        transition:fade
        on:click={slideRight}
      >
        <i class="material-icons">keyboard_arrow_right</i>
      </button>
    {/if}
  </div>
</div>

<style>
  .carousel-container {
    margin: 30px;
    width: 100%;
    max-width: 1200px;
  }

  .album-carousel {
    position: relative;
    display: flex;
    overflow: hidden;
    margin-bottom: 10px;
  }

  .carousel-items {
    padding: 10px;
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
    position: absolute;
    width: 80px;
    z-index: 2;
    border: none;
    opacity: 0;
    animation: invisible .4s ease-out forwards;
  }
  
  .previous-button{
    left: 0;
    background: linear-gradient(-90deg, hsl(0, 0%, 0%, 0%), hsl(0, 0%, 0%, 40%));
  }

  .next-button {
    right: 0;
    background: linear-gradient(90deg, hsl(0, 0%, 0%, 0%), hsl(0, 0%, 0%, 40%));
  }

  .material-icons { 
    color: rgba(255, 255, 255, 1);
    font-size: 48px;
  }
 
  .album-carousel:hover button {
    animation: visible .4s ease-out forwards, lighten .4s ease-out forwards
  }

  .album-carousel:hover button:hover {
    animation: darken .4s ease-out forwards, visible .4s ease-out forwards;
  }

  button:hover .material-icons {
    font-size: 52px;
  }

  @keyframes darken {
    0% {
      background-color: hsl(0, 0%, 0%, 0%);
    }

    100% {
      background-color: hsl(0, 0%, 0%, 10%);
    }
  }
 
  @keyframes lighten {
    0% {
      background-color: hsl(0, 0%, 0%, 10%);
    }

    100% {
      background-color: hsl(0, 0%, 0%, 0%);
    }
  }
  
  @keyframes visible {
    0% {
      opacity: 0;
    }

    100% {
      opacity: 1;
    }
  }
  
  @keyframes invisible {
    0% {
      opacity: 1;
    }

    100% {
      opacity: 0;
    }
  }
</style>