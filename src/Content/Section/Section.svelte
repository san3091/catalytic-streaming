<script>
  import QuickPlayBanner from './QuickPlayBanner/QuickPlayBanner.svelte'
  import ManySection from './ManySection/ManySection.svelte'
  import FewSection from './FewSection/FewSection.svelte'

  export let headerText
  export let sectionDescription
  export let sectionNumber
  export let albums = []
  export let open
  export let updateOpenStates
  let loading
  let selectedAlbum

  $: firstAlbum = albums[1]
  $: lastAlbum = albums[albums.length - 1]
  $: tomorrowAlbum = albums[0]
  $: sectionAlbums = sectionNumber == 0 ? albums.slice(1) : albums

  const selectAlbum = (albumIndex) => {
    loading = true
    updateOpenStates(sectionNumber)
    
    const selectedIndex = albums.findIndex(album => album.index == albumIndex)
    selectedAlbum = albums[selectedIndex]
    
    SC.oEmbed(selectedAlbum.url, {
      auto_play: true,
      color: selectedAlbum.color
    })
    .then((newAlbum) => { loading = false })
    .catch(error => { console.log(error) })
  }
</script>


{#if albums.length}
  <ManySection 
    albums={sectionAlbums}
    headerText={headerText}
    sectionDescription={sectionDescription}
    loading={loading}
    selectAlbum={selectAlbum}
    selectedAlbum={selectedAlbum || sectionAlbums[0]}
    open={open} />

{/if} 

<style>
</style>