<script>
  import QuickPlayBanner from './QuickPlayBanner/QuickPlayBanner.svelte'
  import Carousel from './Carousel/Carousel.svelte'
  import CurrentAlbum from './CurrentAlbum/CurrentAlbum.svelte'
  import FewSection from './FewSection/FewSection.svelte'

  export let headerText
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
  <Carousel 
    albums={albums} 
    headerText={headerText}
    selectAlbum={selectAlbum} />
  <CurrentAlbum 
    selectedAlbum={selectedAlbum || albums[0]} 
    open={open}
    loading={loading} />
{:else}
  <FewSection 
    albums={albums}
    headerText={headerText}
    loading={loading}
    selectAlbum={selectAlbum}
    selectedAlbum={selectedAlbum || albums[0]} />
{/if}

<style>
</style>