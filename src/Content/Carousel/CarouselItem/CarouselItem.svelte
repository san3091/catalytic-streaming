<script>
  import { fade } from 'svelte/transition'

  export let album
  export let selectAlbum
</script>

  {#if !album.loading}
    <div transition:fade class='carousel-item' on:click={ selectAlbum(album.index) } >
      <img src={album.thumbnail_url} />
      <div class='album-info'>
        <h5>{album.title}</h5>
        <h6>{album.author_name}</h6>
      </div>
    </div>
  {/if}

<style>
  .carousel-item {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    height: 210px;
    min-width: 150px;
    background-color: white;
    margin: 10px;
    padding: 10px;
    cursor: pointer;
    box-shadow: 1px 1px 0 black;
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
</style>