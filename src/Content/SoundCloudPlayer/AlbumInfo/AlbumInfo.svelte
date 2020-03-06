<script>
  export let albumInfo
</script>

<div>
  {#if albumInfo}
    <h1>{albumInfo.title}</h1>
    <h3>{albumInfo.author_name}</h3>
    <p>
      {albumInfo.description}
    </p>
  {/if}
</div>

<style>
  div {
    width: 50%;
    background-color: darkgray;
  }
</style>