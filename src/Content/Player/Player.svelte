<script>
  import { tweened } from 'svelte/motion'
  import { cubicOut } from 'svelte/easing'
  
  let open = false
  let width = tweened(50, { easing: cubicOut, duration: 400 })

  const toggleOpen = () => {
    open ? width.set(50) : width.set(1000)
    open = !open
  }

</script>

<div class='player' style='--width:{$width}px'>
  {#if open}
    <button class='close-button' on:click={toggleOpen}>
      <i class="material-icons">close</i>
    </button>
  {/if}
  <button class='slide-button' on:click={toggleOpen} >
    {#if open}
      <i class="material-icons">keyboard_arrow_right</i>
    {:else}
      <i class="material-icons">keyboard_arrow_left</i>
    {/if}
  </button>
</div>

<style>
  .player {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    position: relative;
    width: var(--width);
    border-left: 1px solid #3e3e3e;
  }

  button, button:active {
    background-color: transparent;
    cursor: pointer;
    border: none;
  }

  .close-button {
    position: absolute;
    top: 0;
    right: 0;
  }

  .slide-button {
    height: 100%;
  }

  .material-icons {
    margin: 10px;
    font-size: 28px;
  }

  
</style>