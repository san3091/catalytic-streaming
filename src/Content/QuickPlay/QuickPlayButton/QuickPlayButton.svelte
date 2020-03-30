<script>
  import { fade } from 'svelte/transition'

  export let album
  export let buttonLabel
  export let selectAlbum
  export let selected
</script>

<div class='quickplay-item'>
  <h3>{buttonLabel}</h3>
  <div class='button-container'>
    <button
      transition:fade
      class:selected
      style='--color:{album.color || "#666a86"}'
      on:click={selectAlbum(album)} >
      <div class='button-text'>
        <h5>{album.title}</h5>
        <h6>{album.author_name}</h6>
      </div>
      <img src={album.thumbnail_url} />
    </button>
  </div>
</div>

<style>

.quickplay-item {
    margin-right: 20px;
  }

  h3 {
    margin: 0 10px 10px;
  }
  .button-container {
    position: relative;
  }

  button {
    display: flex;
    flex-direction: row;
    background-color: var(--color);
    border: none;
  }

  img {
    height: 100px;
    width: 100px;
  }

  .button-text {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 20px;
    background-color: hsl(0, 0%, 0%, 50%);
  }

  .button-text * {
    color: #dbdedf;
  }
  
  button::after {
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

  button:hover{
    top: -2px;
    left: -2px;
  }

  button:hover::after {
    top: 6px;
    left: 6px;
  }

  .selected, button.selected:hover {
    top: -4px;
    left: -4px;
  }

  .selected::after, button.selected:hover::after {
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