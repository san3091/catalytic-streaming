<script>
  import { tweened } from 'svelte/motion'
  export let albums
  export let selectAlbum
  let carouselWidth, itemsWidth
  let groupedAlbums = []
  let currentGroupIndex = 0
  let carouselOffset = tweened(0)

  const groupAlbums = (albums) => {
    let groups = [[]]
    albums.forEach((album, index) => {
      const lastGroup = groups[groups.length - 1]
      if (lastGroup.length < 9) {
        lastGroup.push(album)
      } else {
        groups.push([album])
      }
    })
    return groups
  }

  const maxIndex = () => groupedAlbums.length - 1
  
  const previousGroup = () => {
    const nextOffset = $carouselOffset + (carouselWidth - 145)
    console.log(nextOffset)
    nextOffset < 0
      ? carouselOffset.set(nextOffset)
      : carouselOffset.set(0)
  }

  const nextGroup = () => {
    const overflowLength = itemsWidth - carouselWidth
    const nextOffset = $carouselOffset - (carouselWidth - 145)

    overflowLength < -nextOffset
      ? carouselOffset.set(0 - overflowLength)
      : carouselOffset.set(nextOffset)
  }

  $: groupedAlbums = groupAlbums(albums)
</script>

	<h4>Current Selections</h4>
  <div 
    class='album-carousel'
    bind:clientWidth={carouselWidth}>
    {#if $carouselOffset}
      <button 
        class='previous-button'
        on:click={previousGroup}
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
    <button 
      class='next-button'
      on:click={nextGroup}
    >right
    </button>
  </div>

<style>
  .album-carousel {
    position: relative;
    display: flex;
    background-color: lightgray;
    overflow: hidden;
  }

  .carousel-items {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    position: relative;
    left: var(--carousel-offset);
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