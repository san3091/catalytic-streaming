<script>
  import { fade } from 'svelte/transition'
  export let album
</script>

<div class='info-container'>
  {#if album}
    <div 
      class='info-content' 
      transition:fade
      style='--color:{album.color}'
      >
      <h3>{album.title}</h3>
      <h4>{album.author_name}</h4>
      <p>
        {album.description}
      </p>
    </div>
  {/if}
</div>

<style>
  .info-container {
    width: 100%;
  }

  .info-content {
    padding: 20px;
    border: 2px solid #222;
    background-color: hsl(0, 0%, 100%, 80%);
  }

  h4 {
    margin-bottom: 20px;
  }
</style>