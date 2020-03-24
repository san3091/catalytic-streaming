<script>
  import Carousel from './Carousel/Carousel.svelte'
  import CurrentAlbum from './CurrentAlbum/CurrentAlbum.svelte'

  export let albums
  export let headerText
  export let loading
  export let selectAlbum
  export let selectedAlbum
  export let open
</script>

<div>
  <h2>{headerText}</h2>
  <Carousel 
    albums={albums} 
    headerText={headerText}
    selectAlbum={selectAlbum} 
    selectedAlbum={selectedAlbum || albums[0]} />
  <CurrentAlbum 
    selectedAlbum={selectedAlbum || albums[0]} 
    open={open}
    loading={loading} />
</div>

<style>

  h2 {
    align-self: flex-start;
  }

  div {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 1200px;
  }
</style>