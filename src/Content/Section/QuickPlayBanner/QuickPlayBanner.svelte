<script>
  import { fade } from 'svelte/transition'
  export let selectAlbum
  export let firstAlbum
  export let lastAlbum
  export let tomorrowAlbum
</script>

<div class='banner-container'>
  <div class='quick-play-banner'>
    <div 
      class='new-today button' 
      on:click={selectAlbum(firstAlbum.index, 0)}
    >
      {#if firstAlbum }
        <div class='quick-play-label' style='--color:{firstAlbum.color}'>
          <h2>New Today</h2>
        </div>
        <div class='section-content button-content'>
          <h2>{firstAlbum.title}</h2>
          <p>{firstAlbum.author_name}</p>
        </div>
        <img transition:fade src={firstAlbum.thumbnail_url} />
      {/if}
    </div>
    <div class='upcoming-and-dont-miss'>
      <div 
        class='dont-miss button' 
        on:click={selectAlbum(lastAlbum.index, 0)}
      >
        {#if lastAlbum}
          <div class='quick-play-label' style='--color:{lastAlbum.color}'>
            <h2>Don't Miss</h2>
          </div>
          <div class='section-content button-content'>
            <h2>{lastAlbum.title}</h2>
            <p>{lastAlbum.author_name}</p>
          </div>
          <img transition:fade src={lastAlbum.thumbnail_url} />
        {/if}
      </div>
      <div class='upcoming'>
        {#if tomorrowAlbum}
          <div class='quick-play-label'>
            <h2>Tomorrow</h2>
          </div>
          <div class='section-content'>
            <h2>{tomorrowAlbum.title}</h2>
            <p>{tomorrowAlbum.author_name}</p>
          </div>
          <img 
            transition:fade
            class='tomorrow-album-img'
            src={tomorrowAlbum.thumbnail_url} />
        {/if}
      </div>
    </div>
  </div>
</div>

<style>

  h2 {
    margin: 0;
  }

  .banner-container {
    display: flex;
    justify-content: center;
    background-color: #222;
    width: 100%;
    border: 1px solid #222;
    margin-bottom: 40px;
  }

  .button {
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    box-sizing: border-box;
    border: 1px solid #222;
  }

  .button-content {
    background: linear-gradient(0deg, hsl(0, 0%, 0%, 60%), hsl(0, 0%, 0%, 0%));
  }

  .button-content * {
    color: white;
  }
  
  .section-content {
    position: absolute;
    width: 100%;
    left: 0;
    bottom: 0;
    padding: 20px;
  }

  .section-content * {
    margin: 0;
  }

  .section-content h2 {
    width: 370px;
  }

  img {
    width: 100%;
    z-index: -3;
  }


  .tomorrow-album-img {
    position: absolute;
    right: 10px;
    top: 10px;
    z-index: 1;
    height: 180px;
    width: 180px;
  }

 .quick-play-banner {
    display: flex;
    flex-direction: row;
    height: 400px;
    width: 100%;
    max-width: 1500px; 
  }

  .new-today {
    position: relative;
    width: 60%;
    height: 100%;
    cursor: pointer;
    overflow: hidden;
    z-index: 1;
  }

  .upcoming-and-dont-miss {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 40%;
  }

  .dont-miss {
    position: relative;
    overflow: hidden;
    height: 50%;
    cursor: pointer;
    z-index: 1;
  }

  .upcoming {
    box-sizing: border-box;
    position: relative;
    height: 50%;
    background-color: #f96854;
    border: 1px solid #222;

  }

  .quick-play-label {
    position: absolute;
    top: 20px;
    left: 20px;
    padding: 20px;
    background-color: white;
  }

  .quick-play-label::before {
    content: '';
    position: absolute;
    background-color: var(--color);
    top: 3px;
    left: 3px;
    height: 100%;
    width: 100%;
    z-index: -1;
  }
  
  .quick-play-label::after {
    content: '';
    position: absolute;
    background-color: black;
    top: 6px;
    left: 6px;
    height: 100%;
    width: 100%;
    z-index: -2;
  }

  .button:hover .quick-play-label {
    top: 18px;
    left: 18px;
  }
  
  .button:hover .quick-play-label::after {
    top: 8px;
    left: 8˝px;
  }
</style>