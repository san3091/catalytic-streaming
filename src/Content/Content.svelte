<script>
  import { onMount } from 'svelte'

  import Section from './Section/Section.svelte'

  const albumURLs = [
    'https://soundcloud.com/user-861231864/sets/streaming-test-1/s-q4DAH',
    'https://soundcloud.com/playlist/sets/love-hurts',
    'https://soundcloud.com/soundcloud-hustle/sets/hip-hop-party-starters',
    'https://soundcloud.com/soundcloud-hustle/sets/hip-hop-love-songs',
    'https://soundcloud.com/soundcloud-hustle/sets/mac-millers-definitive-1',
    'https://soundcloud.com/soundcloud-shine/sets/chill-pop',
    'https://soundcloud.com/soundcloud-shine/sets/playback-2019',
    'https://soundcloud.com/soundcloud-shine/sets/2019-shine-playback',
    'https://soundcloud.com/badbunny15/sets/yhlqmdlg-1',
    'https://soundcloud.com/badbunny15/sets/x-100pre-2',
    'https://soundcloud.com/soundcloud-the-peak/sets/midnight-dark-electro',
    'https://soundcloud.com/soundcloud-the-peak/sets/atmospheric-edm',
    'https://soundcloud.com/fresh-pressed/sets/fresh-pressed-tracks',
    'https://soundcloud.com/user-861231864/sets/streaming-test-1/s-q4DAH',
    'https://soundcloud.com/soundcloud-scenes/sets/psychedelic-indie',
    'https://soundcloud.com/monstercat/sets/monstercat-instinct',
    'https://soundcloud.com/monstercat/sets/dream-in-color-the-remixes',
    'https://soundcloud.com/soundcloud-la-onda/sets/tropical-pop',
    'https://soundcloud.com/soundcloud-la-onda/sets/rap-en-espanol',
    'https://soundcloud.com/soundcloud-la-onda/sets/afro-latinx-diaspora',
    'https://soundcloud.com/soundcloud-la-onda/sets/amor-norteno-love-ballads',
    'https://soundcloud.com/soundcloud-circuits/sets/equalizers-female-electronic-producers',
    'https://soundcloud.com/soundcloud-circuits/sets/zero-in-electronic-deep-focus',
    'https://soundcloud.com/soundcloud-mainroom/sets/dance-new-hot',
    'https://soundcloud.com/soundcloud-mainroom/sets/jack-chicago-house-icons',
    'https://soundcloud.com/soundcloud-mainroom/sets/the-sounds-of-acid',
    'https://soundcloud.com/soundcloud-mainroom/sets/a-history-of-detroit-techno',
    'https://soundcloud.com/soundcloud-mainroom/sets/divas-women-of-house-music',
    'https://soundcloud.com/soundcloud-shine/sets/chill-pop',
    'https://soundcloud.com/soundcloud-scenes/sets/dreamo-emo-indie-rap',
    'https://soundcloud.com/soundcloud-auras/sets/queen-things-women-of-r-b'
  ]

  let albums = []
  let openStates = [false, false, false]

  const caaAlbums = (albums) => {
    const albumsCopy = albums.slice(3, 22).map(album => {
      const albumCopy = Object.assign({}, album)
      albumCopy.color = "#588b8b"
      return albumCopy
    })
    return albumsCopy
  }
  
  const hwhAlbums = (albums) => {
    const albumsCopy = albums.slice(24, 29).map(album => {
      const albumCopy = Object.assign({}, album)
      albumCopy.color = "#be3e82"
      return albumCopy
    })
    return albumsCopy
  }

  const loadAlbumData = (index=0) => {
    albumURLs.forEach((url, index) => {
      // const color = albumColor(index)
      
      albums.push({ loading: true })
      SC.oEmbed(albumURLs[index])
      .then(newAlbum => {
        newAlbum.url = url
        // newAlbum.color = color
        newAlbum.index = index
        albums[index] = newAlbum
      })
    })
  }

  const updateOpenStates = (sectionNumber) => {
    openStates.forEach((state, index) => { 
      index == sectionNumber
       ? openStates[index] = true
       : openStates[index] = false
    })
  }

  onMount(() => {
    loadAlbumData()
  })
</script>

<div class='content'>
  <Section
    headerText='Rotating Selection'
    sectionDescription='Explore a rotating selection of free jazz. Find a new album every day.'
    sectionNumber={0}
    albums={albums}
    open={openStates[0]} 
    updateOpenStates={updateOpenStates} />
  <Section 
    headerText='Catalytic Artist Albums'
    sectionDescription='Discover artists represented by Catalytic Sound.'
    sectionNumber={1}
    albums={caaAlbums(albums)}
    open={openStates[1]} 
    updateOpenStates={updateOpenStates} />
  <Section 
    headerText="History is What's Happening"
    sectionDescription='Experience an artist curated selection of pre-2000s free jazz.'
    sectionNumber={2}
    albums={hwhAlbums(albums)}
    open={openStates[2]} 
    updateOpenStates={updateOpenStates} />
</div>

<style>
  .content {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
  }
</style>