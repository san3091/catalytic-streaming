<script>
  import Carousel from './Carousel/Carousel.svelte'

  export let albums
  export let headerText
  export let sectionDescription
  export let selectAlbum
  export let selectedAlbum
  export let rotating

  let width
  $: padding = (width > 1300) ? '100px' : '50px'
</script>

<div bind:clientWidth={width} style='--padding:{padding}' >
  <h2>{headerText}</h2>
  <p>{sectionDescription}</p>
  <Carousel 
    albums={albums} 
    selectAlbum={selectAlbum} 
    selectedAlbum={selectedAlbum}
    rotating={rotating} />
</div>

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