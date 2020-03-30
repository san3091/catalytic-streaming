<script>
  import { tweened } from 'svelte/motion'
  import { cubicOut } from 'svelte/easing'
  import { fade } from 'svelte/transition'
  import AlbumTile from '../../AlbumTile/AlbumTile.svelte'
  import ProgressIndicator from './ProgressIndicator/ProgressIndicator.svelte'

  export let albums
  export let selectAlbum
  export let selectedAlbum

  let carouselWidth, itemsWidth
  let currentSection = 0
  let resizing = false
  let carouselOffset = tweened(0, { easing: cubicOut })
  let tileWidth = tweened(0, { easing: cubicOut, duration: 400 })

  const scroll = (currentSection, widthChange=false) => {
    if (scrollable) {
      const newScrollPosition = currentSection * carouselWidth
      
      if ((newScrollPosition + carouselWidth) > itemsWidth) {
          carouselOffset.set(itemsWidth - carouselWidth)
      } else {
        carouselOffset.set(currentSection * carouselWidth)
      }
    }
  }

  const calcSections = (itemsWidth) => {
    let sections = 0
    if (itemsWidth && carouselWidth) {
      sections = Math.ceil(itemsWidth / carouselWidth)
    }
    return sections
  }

  const previousSection = () => {
    if (currentSection > 0) { currentSection -= 1 }
    scroll(currentSection)
  }

  const nextSection = () => {
    if (currentSection < numberOfSections) { currentSection += 1 }
    scroll(currentSection)
  }

  const resizeTiles = async (carouselWidth) => {
    resizing = true
    await tileWidth.set((carouselWidth / 6), { delay: 200 })
    resizing = false
  }

  $: scrollable = itemsWidth > carouselWidth
  $: resizeTiles(carouselWidth)
  $: numberOfSections = calcSections(itemsWidth)
  $: if (carouselWidth || resizing) { scroll(currentSection, true) }
</script>

<div class='carousel-container'>
  {#if scrollable }
    <ProgressIndicator 
      numberOfSections={numberOfSections}
      currentSection={currentSection} />
  {/if}
  <div 
    class='album-carousel'
    class:scrollable
    bind:clientWidth={carouselWidth}>
    {#if currentSection > 0}
      <button 
        class='previous-button'
        transition:fade
        on:click={previousSection}
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
          selected={selectedAlbum == album}
          tileWidth={$tileWidth} />
      {/each}
    </div>
    {#if currentSection < (numberOfSections - 1) }
      <button 
        class='next-button'
        transition:fade
        on:click={nextSection}
      >
        <i class="material-icons">keyboard_arrow_right</i>
      </button>
    {/if}
  </div>
</div>

<style>
  .carousel-container {
    position: relative;
    margin-bottom: 40px;
    width: 100%;
  }
  
  .album-carousel {
    position: relative;
    display: flex;
    overflow: hidden;
  }

  .carousel-items {
    position: relative;
    display: flex;
    flex-direction: row;
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
    /* background: linear-gradient(-90deg, hsl(0, 0%, 0%, 0%), rgb(249, 104, 84, 0.4)); */
    background: linear-gradient(-90deg, hsl(0, 0%, 0%, 0%), hsl(0, 0%, 0%, 40%));
  }

  .next-button {
    right: 0;
    /* background: linear-gradient(90deg, hsl(0, 0%, 0%, 0%), rgb(249, 104, 84, 0.4)); */
    background: linear-gradient(90deg, hsl(0, 0%, 0%, 0%), hsl(0, 0%, 0%, 40%));
  }

  .material-icons { 
    color: rgba(255, 255, 255, 1);
    font-size: 48px;
  }
 
  .scrollable:hover button {
    animation: visible .4s ease-out forwards, lighten .4s ease-out forwards
  }

  .scrollable:hover button:hover {
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