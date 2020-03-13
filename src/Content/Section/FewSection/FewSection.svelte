<script>
  import { tweened } from 'svelte/motion'
  import AlbumTile from '../AlbumTile/AlbumTile.svelte'
  import AlbumInfo from '../AlbumInfo/AlbumInfo.svelte'
  import SoundCloudPlayer from '../SoundCloudPlayer/SoundCloudPlayer.svelte'
  export let albums
  export let headerText
  export let open
  export let loading
  export let selectAlbum
  export let selectedAlbum
  let playerWidth = tweened(0)
  let width = tweened(null)

  $: playerWidth.set(open ? 680 : 0)
  $: width.set(open || albums.length < 5 ? 400 : 580)
</script>

<div class='few-section' 
>
  <h3>{headerText}</h3>
  <div class='few-section-content'>
    <div 
      class='albums' 
      style='--width:{$width}px;'>
      {#each albums as album}
        <AlbumTile
          album={album}
          selectAlbum={selectAlbum} />
      {/each}
    </div>
    
    {#if open}
      <div class='player' style='--player-width:{$playerWidth}px'>
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
    display: flex;
    flex-direction: column;
    margin: 20px;
    box-sizing: border-box;
  }

  .few-section-content {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    background-color: beige;
    padding: 30px;
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
    padding: 15px 30px 0 30px;
    width: var(--player-width);
  }

  .info-container {
    padding-bottom: 20px;
  }
</style>