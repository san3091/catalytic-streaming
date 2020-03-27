<script>
  export let itemsWidth
  export let slideDistance
  export let carouselOffset

  let numberOfSections = 0
  let defaultDashColor = "#dbdedf"
  let activeDashColor = "#3e3e3e"
  // let activeDashColor = "#f96854"

  const iterableDashes = (numberOfSections) => {
    return [...Array(numberOfSections).keys()]
  }

  const calcSections = (itemsWidth, slideDistance) => {
    let sections = 0
    if (itemsWidth && slideDistance) {
      sections = Math.ceil(itemsWidth / slideDistance)
    }
    return sections
  }

  $: numberOfSections = calcSections(itemsWidth, slideDistance)
  $: indicatorLength = numberOfSections * 30 + 10
  $: dashes = iterableDashes(numberOfSections)
  $: currentSection = Math.ceil(carouselOffset / slideDistance)
</script>

<svg viewBox="0 0 {indicatorLength} 20" class='progress-indicator' style='--width:{indicatorLength}'>
  {#each dashes as { id, dash }, i}
    <line 
      x1={10 + i * 30} y1="10" 
      x2={30 + i * 30} y2="10" 
      stroke={i == currentSection ? activeDashColor : defaultDashColor} />
  {/each}
</svg>

<style>
  .progress-indicator {
    position: absolute;
    right: 0;
    top: -20px;
    height: 20px;
    width: var(--width);
  }

  line {
    stroke-width: 4;
  }
</style>