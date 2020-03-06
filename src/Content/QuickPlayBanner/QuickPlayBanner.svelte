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
      <div class='quick-play-header'>
        <h2>New Today</h2>
      </div>
    </div>
    <div class='upcoming-and-dont-miss'>
      <div 
        class='dont-miss' 
        style='--last-album-img:url({lastAlbum && lastAlbum.thumbnail_url});'
        on:click={selectAlbum(lastAlbum.index)}
      >
        <div class='quick-play-header'>
          <h2>Don't Miss</h2>
        </div>
      </div>
      <div class='upcoming'>
        <div class='quick-play-header'>
          <h2>Coming Tomorrow</h2>
        </div>
      </div>
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
    position: relative;
    width: 60%;
    height: 100%;
    background-image: var(--first-album-img);
    cursor: pointer;
  }

  .upcoming-and-dont-miss {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 40%;
    background-color: brown;
  }

  .dont-miss {
    position: relative;
    background-image: var(--last-album-img);
    height: 50%;
    cursor: pointer;
  }
  .upcoming {
    position: relative;
    background-color: yellow;
    height: 50%;
  }

  .quick-play-header {
    position: absolute;
    top: 20px;
    left: 20px;
    padding: 20px;
    background-color: white;
    box-shadow: 1px 1px 0 black;
  }
</style>