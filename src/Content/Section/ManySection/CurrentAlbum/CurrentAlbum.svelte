<script>
  import { slide } from 'svelte/transition'
  import SoundCloudPlayer from '../../SoundCloudPlayer/SoundCloudPlayer.svelte'
  import AlbumInfo from '../../AlbumInfo/AlbumInfo.svelte'

  export let selectedAlbum
  export let loading
  export let open
  let albumInfo
</script>

{#if open}
  <div transition:slide class='current-album-container'>
    <div class='current-album'>
      <div class='player'>
        <SoundCloudPlayer 
          selectedAlbum={selectedAlbum} 
          loading={loading} />
      </div>
      <div class='info-container'>
        <AlbumInfo album={selectedAlbum} />
      </div>
    </div>
  </div>
{/if}

<style>
  .current-album-container {
  	box-sizing: border-box;
    width: 100%;
    padding: 0 40px 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .current-album {
    display: flex;
    width: 100%;
    flex-direction: row;
    justify-content: center;
  }

  .player {
    width: 50%;
  }

  .info-container {
    padding-left: 40px;
    width: 50%;
  }
</style>