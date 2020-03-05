<script>
  import { onMount } from 'svelte'
  import Carousel from './Carousel/Carousel.svelte'
  import SoundCloudPlayer from './SoundCloudPlayer/SoundCloudPlayer.svelte'

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

  let selectedAlbumURL = albumURLs[0]
  let albums = []

  const loadAlbumData = (index=0) => {
    const maxIndex = albumURLs.length - 1
    const nextIndex = index + 1
    SC.oEmbed(albumURLs[index], {})
    .then((newAlbum) => {
      newAlbum.index = index
      albums = [...albums, newAlbum]
      if (nextIndex <= maxIndex) { loadAlbumData(nextIndex) }
    })
  }

  const selectAlbum = (albumIndex) => {
    selectedAlbumURL = albumURLs[albumIndex]
  }

  onMount(() => {
    loadAlbumData()
  })
</script>

<main>
  <Carousel albums={albums} selectAlbum={selectAlbum} />
  <SoundCloudPlayer selectedAlbumURL={selectedAlbumURL} />
</main>

<style>
</style>