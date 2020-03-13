<script>
  import AlbumTile from '../AlbumTile/AlbumTile.svelte'
  import AlbumInfo from '../AlbumInfo/AlbumInfo.svelte'
  import SoundCloudPlayer from '../SoundCloudPlayer/SoundCloudPlayer.svelte'
  export let albums
  export let headerText
  export let open
  export let loading
  export let selectAlbum
  export let selectedAlbum

  $: sectionWidth = open ? 1200 : null
  $: width = open || albums.length < 5 ? 400 : 580
</script>

<div class='few-section' style='--section-width:{sectionWidth}px'>
  <h3>{headerText}</h3>
  <div class='few-section-content'>
    <div 
      class='albums' 
      style='--width:{width}px;'>
      {#each albums as album}
        <AlbumTile
          album={album}
          selectAlbum={selectAlbum} />
      {/each}
    </div>
    
    {#if open}
      <div class='player'>
        <div class='info-container'>
          <AlbumInfo album={selectedAlbum} />
        </div>
        <SoundCloudPlayer 
          selectedAlbum={selectedAlbum} 
          loading={loading} />
      </div>
    {/if}
  </div>
</div>

<style>
  .few-section {
    padding: 30px;
    display: flex;
    flex-direction: column;
    margin: 20px;
    box-sizing: border-box;
    width: var(--section-width);  
    background-color: beige;
  }

  .few-section-content {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }

  .albums {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: flex-start;
    margin-left: -15px;
    width: var(--width);
  }

  .player {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    padding: 15px 30px 0 30px;
  }

  .info-container {
    padding-bottom: 20px;
  }
</style>