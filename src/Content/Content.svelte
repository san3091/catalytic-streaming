<script>
  import { onMount } from 'svelte'

  import Section from './Section/Section.svelte'

  const albumURLs = [
    // 'https://soundcloud.com/user-861231864/sets/streaming-test-1/s-q4DAH',
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
  let openStates = [true, false, false, false]

  const albumColor = (index) => {
    let color 
    if (index == 0) { 
      color = '#FFFF00'
    } else if (index == albumURLs.length - 1) { 
      color = '#FF0000' 
    } else { color = '#734f96' }
    return color
  }


  const loadAlbumData = (index=0) => {
    albumURLs.forEach((url, index) => {
      const color = albumColor(index)
      
      albums.push({ loading: true })
      SC.oEmbed(albumURLs[index], {color})
      .then(newAlbum => {
        newAlbum.url = url
        newAlbum.color = color
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
    headerText='Rotating Seclection'
    sectionNumber={0}
    albums={albums}
    open={openStates[0]} 
    updateOpenStates={updateOpenStates} />
  <Section 
    headerText='Tag 1'
    sectionNumber={1}
    albums={albums.slice(2, 18)}
    open={openStates[1]} 
    updateOpenStates={updateOpenStates} />
  <Section 
    headerText='Tag 2'
    sectionNumber={2}
    albums={albums.slice(6, 37)}
    open={openStates[2]} 
    updateOpenStates={updateOpenStates} />
  <Section 
    headerText='Tag 3'
    sectionNumber={3}
    albums={albums.slice(15, 19)}
    open={openStates[3]} 
    updateOpenStates={updateOpenStates} />
  <Section 
    headerText='Tag 4'
    sectionNumber={4}
    albums={albums.slice(15, 17)}
    open={openStates[4]} 
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