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

  $: width = albums.length <= 4 ? 380 : 570
</script>

<div class='few-section'>
  <div class='left-content'>
    <h2>{headerText}</h2>
    <div class='album-container'>
      <div class='albums' style='--width:{width}px'>
        {#each albums as album}
          <AlbumTile
            album={album}
            selectAlbum={selectAlbum}
            selected={album == selectedAlbum} />
        {/each}
      </div>
    </div>
  </div>
    
  <div class='player'>
    <div class='info-container'>
      <AlbumInfo 
        album={selectedAlbum} />
    </div>
    <SoundCloudPlayer 
      selectedAlbum={selectedAlbum} 
      loading={loading} />
  </div>
</div>

<style>
  .few-section {
    width: 1200px;
    display: flex;
    flex-direction: row;
  }

  .left-content {
    display: flex;
    flex-direction: column;
  }

  .albums {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    width: var(--width);
  }

  .player {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    padding: 45px 30px 30px;
  }

  .info-container {
    padding-bottom: 30px;
  }
</style>