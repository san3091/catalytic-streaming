<script>
  import { fade } from 'svelte/transition'
  export let albumInfo
  export let loading

</script>

<div class='info-container'>
  {#if albumInfo && !loading}
    <div transition:fade>
      <h1>{albumInfo.title}</h1>
      <h3>{albumInfo.author_name}</h3>
      <p>
        {albumInfo.description}
      </p>
    </div>
  {/if}
</div>

<style>
  .info-container {
    padding: 20px;
    width: 40%;
  }
</style>