<script>
  import { fade } from 'svelte/transition'
  export let albumInfo
  export let loading

</script>

<div class='info-container'>
  {#if albumInfo && !loading}
    <div class='info-content' transition:fade>
      <h1>{albumInfo.title}</h1>
      <h4>{albumInfo.author_name}</h4>
      <p>
        {albumInfo.description}
      </p>
    </div>
  {/if}
</div>

<style>
  .info-container {
    padding: 20px 0 10px 10px;
    width: 50%;
  }

  .info-content {
    padding: 20px;
    border: 2px solid orange;
  }

  h4 {
    margin-bottom: 20px;
  }
</style>