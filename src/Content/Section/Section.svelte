<script>
  import ManySection from './ManySection/ManySection.svelte'

  export let headerText
  export let sectionDescription
  export let sectionNumber
  export let selectedAlbum
  export let selectAlbum
  export let albums = []


  $: sectionAlbums = sectionNumber == 0 ? albums.slice(1) : albums
</script>


{#if albums.length}
  <ManySection 
    albums={sectionAlbums}
    headerText={headerText}
    sectionDescription={sectionDescription}
    selectAlbum={selectAlbum}
    selectedAlbum={selectedAlbum}
    rotating={sectionNumber == 0} />
{/if} 

<style>
</style>