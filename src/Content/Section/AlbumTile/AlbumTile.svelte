<script>
  import { fade } from 'svelte/transition'

  export let album
  export let selectAlbum
  export let selected
</script>

<div class='tile-container'>
  {#if !album.loading}
    <div 
      transition:fade
      class='album-tile'
      class:selected
      style='--color:{album.color || "#666a86"}'
      on:click={ selectAlbum(album) } >
      <img src={album.thumbnail_url} />
      <div class='album-info'>
        <h5>{album.title}</h5>
        <h6>{album.author_name}</h6>
      </div>
    </div>
  {/if}
</div>


<style>
  .tile-container {
    position: relative;
    display: flex;
    z-index: 1;
    margin: 10px;
    margin-bottom: 15px;
  }

  .album-tile {
    display: flex;
    flex-direction: column;
    width: 200px;
    cursor: pointer;
    background-color: var(--color);
  }
  
  .album-tile::after {
    content: '';
    position: absolute;
    background-color: #222;
    opacity: 0;
    top: 4px;
    left: 4px;
    height: 100%;
    width: 100%;
    z-index: -2;
    animation: fade-in 1s 0.5s ease-in forwards;
  }

  .album-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    height: 100%;
    padding: 10px;
    background-color: hsl(0, 0%, 0%, 50%);
  }

  .album-info * {
    color: #dbdedf;
  }
  
  img {
    height: 200px;
    width: 200px;
  }

  .album-tile:hover{
    top: -2px;
    left: -2px;
  }

  .album-tile:hover::after {
    top: 6px;
    left: 6px;
  }

  .selected, .album-tile.selected:hover {
    top: -4px;
    left: -4px;
  }

  .selected::after, .album-tile.selected:hover::after {
    top: 8px;
    left: 8px;
  }

  @keyframes fade-in {
    0% {
      opacity: 0;
      background-color: transparent;
    }
    50% {
      background-color: transparent;
    }
    100% {
      opacity: 1;
    }
  }
</style>