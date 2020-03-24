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

  $: firstAlbum = albums[0]
  $: lastAlbum = albums[albums.length - 1]

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

{#if sectionNumber == 0}
  <QuickPlayBanner 
  selectAlbum={selectAlbum}
  firstAlbum={firstAlbum}
  lastAlbum={lastAlbum}/>
{/if}
{#if albums.length > 6}
  <ManySection 
    albums={albums}
    headerText={headerText}
    sectionDescription={sectionDescription}
    loading={loading}
    selectAlbum={selectAlbum}
    selectedAlbum={selectedAlbum || albums[0]}
    open={open}
  />
{:else}
  <FewSection 
    albums={albums}
    headerText={headerText}
    sectionDescription={sectionDescription}
    loading={loading}
    selectAlbum={selectAlbum}
    selectedAlbum={selectedAlbum || albums[0]} />
{/if}

<style>
</style>