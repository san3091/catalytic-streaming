<script>
  import { onMount } from 'svelte'
  export let selectedAlbumURL

  onMount(() => {   
    SC.oEmbed(selectedAlbumURL, {
      element: document.getElementById('sound-cloud')
    }).then((embed) => {
      console.log(embed)
    })
  })
</script>

<div>
  <div id='sound-cloud'></div>
</div>

<style>
  div {
    width: 60%;
  }

  #sound-cloud {
    width: 100%;
  }
</style>