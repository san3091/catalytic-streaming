<script>
  import QuickPlayButton from './QuickPlayButton/QuickPlayButton.svelte'
  export let firstAlbum
  export let lastAlbum
  export let selectAlbum
  export let selectedAlbum

</script>

<div class='quickplay'>
  {#if firstAlbum && !firstAlbum.loading}
    <QuickPlayButton 
      album={firstAlbum}
      buttonLabel={'New Today'}
      selectAlbum={selectAlbum}
      selected={selectedAlbum == firstAlbum}
    />
  {/if}
  {#if lastAlbum && !lastAlbum.loading}
    <QuickPlayButton 
      album={lastAlbum}
      buttonLabel={"Don't Miss"}
      selectAlbum={selectAlbum}
      selected={selectedAlbum == lastAlbum}
    />
  {/if}
</div>

<style>
  .quickplay {
    display: flex;
    flex-direction: row;
    margin: 0 100px;
  }
</style>