<script>
  export let albums
  let groupedAlbums = []
  let currentGroupIndex = 0
  
  const groupAlbums = (albums) => {
    let groups = [[]]
    albums.forEach((album, index) => {
      const lastGroup = groups[groups.length - 1]
      if (lastGroup.length < 8) {
        lastGroup.push(album)
      } else {
        groups.push([album])
      }
    })
    return groups
  }

  const maxIndex = () => groupedAlbums.length - 1
  
  const previousGroup = () => {
    currentGroupIndex > 0
      ? currentGroupIndex -= 1
      : currentGroupIndex = maxIndex()
  }

  const nextGroup = () => {
    currentGroupIndex < maxIndex()
      ? currentGroupIndex += 1
      : currentGroupIndex = 0
  }

  $: groupedAlbums = groupAlbums(albums)
</script>

<div>
	<h4>Current Selections</h4>
  <div class='album-carousel'>
    <button on:click={previousGroup}>left</button>
    {#each groupedAlbums[currentGroupIndex] as album}
      <div class='carousel-item'>
        <img src={album.thumbnail_url} />
        <div class='album-info'>
          <h5>{album.title}</h5>
          <h6>{album.author_name}</h6>
        </div>
      </div>
    {/each}
    <button on:click={nextGroup}>right</button>
  </div>
</div>

<style>
  .album-carousel {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    height: 250px;
    background-color: yellowgreen;
  }

  .carousel-item {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    height: 210px;
    width: 150px;
    background-color: aqua;
    margin: 10px;
    padding: 10px;
  }

  .album-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    height: 100%;
    padding: 10px;
  }
  img {
    height: 150px;
    width: 150px;
  }

  button {
    height: 100%;
  }
</style>