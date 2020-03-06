<script>
  export let selectAlbum
  export let firstAlbum
  export let lastAlbum
</script>

<div class='banner-container'>
  <div class='quick-play-banner'>
    <div 
      class='new-today' 
      style='--first-album-img:url({firstAlbum && firstAlbum.thumbnail_url});'
      on:click={selectAlbum(firstAlbum.index)}
    >
    </div>
    <div class='upcoming-and-dont-miss'>
      <div 
        class='dont-miss' 
        style='--last-album-img:url({lastAlbum && lastAlbum.thumbnail_url});'
        on:click={selectAlbum(lastAlbum.index)}
      >
      </div>
      <div class='upcoming'>f</div>
    </div>
</div>
</div>

<style>
  .banner-container {
    display: flex;
    justify-content: center;
    background-color: slategray;
    width: 100%;

  }

 .quick-play-banner {
    display: flex;
    flex-direction: row;
    height: 400px;
    width: 100%;
    max-width: 1500px; 
  }

  .new-today {
    width: 60%;
    height: 100%;
    background-image: var(--first-album-img)
  }

  .upcoming-and-dont-miss {
    
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 40%;
    background-color: brown;
  }

  .dont-miss {
    background-image: var(--last-album-img);
    height: 50%;
  }
  .upcoming {
    background-color: yellow;
    height: 50%;
  }
</style>