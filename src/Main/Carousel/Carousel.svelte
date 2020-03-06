<script>
  import { tweened } from 'svelte/motion'
  export let albums
  export let selectAlbum
  let carouselWidth, itemsWidth
  let carouselOffset = tweened(0)
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
        <div class='carousel-item' on:click={ selectAlbum(album.index) } >
          {#if !album.loading}
            <img src={album.thumbnail_url} />
            <div class='album-info'>
              <h5>{album.title}</h5>
              <h6>{album.author_name}</h6>
            </div>
          {/if}
        </div>
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
    background-color: lightgray;
    overflow: hidden;
  }

  .carousel-items {
    position: relative;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    position: relative;
    right: var(--carousel-offset);
  }
  
  .carousel-item {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    height: 210px;
    min-width: 150px;
    background-color: white;
    border-radius: 5px;
    margin: 10px;
    padding: 10px;
  }

  .album-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    height: 100%;
    padding: 10px;
  }
  img {
    height: 150px;
    width: 150px;
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