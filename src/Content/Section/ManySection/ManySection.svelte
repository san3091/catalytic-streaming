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
  <Carousel 
      albums={albums} 
      headerText={headerText}
      selectAlbum={selectAlbum} />
  <CurrentAlbum 
    selectedAlbum={selectedAlbum || albums[0]} 
    open={open}
    loading={loading} />
</div>

<style>
  div {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 1200px;
    margin: 20px 0 30px 0;
  }
</style>