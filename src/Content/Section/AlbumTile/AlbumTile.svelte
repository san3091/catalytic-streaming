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
      style='--color:{album.color || "#a7a7a7"}'
      on:click={ selectAlbum(album.index) } >
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
    margin-bottom: 35px;
    height: 220px;
    width: 170px;
    background-color: white;
  }

  .album-tile {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    padding: 10px;
    cursor: pointer;
    background-color: white;
  }

  .album-tile::before {
    content: '';
    position: absolute;
    background-color: var(--color);
    top: 3px;
    left: 3px;
    height: 100%;
    width: 100%;
    z-index: -1;
    animation: fade-in 1s ease-in;
  }
  
  .album-tile::after {
    content: '';
    position: absolute;
    background-color: #222;
    opacity: 0;
    top: 6px;
    left: 6px;
    height: 100%;
    width: 100%;
    z-index: -2;
    animation: fade-in 1s 0.5s ease-in forwards;
  }

  .album-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 10px;
  }
  
  img {
    height: 150px;
    width: 150px;
  }

  .album-tile:hover{
    top: -2px;
    left: -2px;
  }

  .album-tile:hover::after {
    top: 8px;
    left: 8px;
  }

  .selected, .album-tile.selected:hover {
    top: -4px;
    left: -4px;
  }

  .selected::after, .album-tile.selected:hover::after {
    top: 10px;
    left: 10px;
  }

  @keyframes fade-in {
    0% {
      opacity: 0;
      background-color: white;
    }
    50% {
      background-color: white;
    }
    100% {
      opacity: 1;
    }
  }
</style>