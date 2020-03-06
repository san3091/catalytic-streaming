<script>
  export let album
  export let selectAlbum
</script>

<div class='carousel-item' on:click={ selectAlbum(album.index) } >
  {#if !album.loading}
    <img src={album.thumbnail_url} />
    <div class='album-info'>
      <h5>{album.title}</h5>
      <h6>{album.author_name}</h6>
    </div>
  {/if}
</div>

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