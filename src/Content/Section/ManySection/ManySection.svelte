<script>
  import Carousel from './Carousel/Carousel.svelte'
  import CurrentAlbum from './CurrentAlbum/CurrentAlbum.svelte'

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
  <CurrentAlbum 
    selectedAlbum={selectedAlbum} 
    open={open}
    loading={loading} />
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
    padding: 0 150px;
  }
</style>