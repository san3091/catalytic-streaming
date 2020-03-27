<script>
  import Carousel from './Carousel/Carousel.svelte'

  export let albums
  export let headerText
  export let sectionDescription
  export let loading
  export let selectAlbum
  export let selectedAlbum
  export let open
</script>

<div>
  <h2>{headerText}</h2>
  <p>{sectionDescription}</p>
  <Carousel 
    albums={albums} 
    headerText={headerText}
    selectAlbum={selectAlbum} 
    selectedAlbum={selectedAlbum} />
</div>

<style>

  h2, p {
    margin-left: 50px;
  }

  div {
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    width: 100%;
    padding: 0 100px;
  }
</style>