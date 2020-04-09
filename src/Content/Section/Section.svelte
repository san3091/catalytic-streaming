<script>
  import Carousel from './Carousel/Carousel.svelte'

  export let headerText
  export let sectionDescription
  export let sectionNumber
  export let selectedAlbum
  export let selectAlbum
  export let albums = []

  let width

  $: padding = (width > 1300) ? '100px' : '50px'
  $: albums = sectionNumber == 0 ? albums.slice(1) : albums
</script>


{#if albums.length}
  <div bind:clientWidth={width} style='--padding:{padding}' >
  <h2>{headerText}</h2>
  <p>{sectionDescription}</p>
  <Carousel 
    albums={albums} 
    selectAlbum={selectAlbum} 
    selectedAlbum={selectedAlbum}
    rotating={sectionNumber == 0} />
  </div>
{/if} 

<style>
 h2, p {
    margin-left: 50px;
  }

  div {
    box-sizing: border-box;
    width: 100%;
    padding: 0 var(--padding);
  }
</style>