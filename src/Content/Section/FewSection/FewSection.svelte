<script>
  import { tweened } from 'svelte/motion'
  import AlbumTile from '../AlbumTile/AlbumTile.svelte'
  import AlbumInfo from '../AlbumInfo/AlbumInfo.svelte'
  import SoundCloudPlayer from '../SoundCloudPlayer/SoundCloudPlayer.svelte'
  export let albums
  export let headerText
  export let loading
  export let selectAlbum
  export let selectedAlbum

  $: width = albums.length <= 4 ? 390 : 580
</script>

<div class='few-section'>
  <h3>{headerText}</h3>
  <div class='few-section-content'>
    <div class='album-container'>
      <div class='albums' style='--width:{width}px'>
        {#each albums as album}
          <AlbumTile
            album={album}
            selectAlbum={selectAlbum} />
        {/each}
      </div>
    </div>
    
    <div class='player'>
      <div class='info-container'>
        <AlbumInfo album={selectedAlbum} />
      </div>
      <SoundCloudPlayer 
        selectedAlbum={selectedAlbum} 
        loading={loading} />
    </div>
  </div>
</div>

<style>
  .few-section {
    margin: 20px;
    width: 1200px;
  }

  .few-section-content {
    display: flex;
    flex-direction: row;
  }

  .albums {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    width: var(--width);
    background-color: beige;
    padding: 20px;
  }

  .player {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    padding: 0 30px 0 30px;
  }

  .info-container {
    padding-bottom: 20px;
  }
</style>