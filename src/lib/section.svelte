<script lang="ts">
  import { onMount } from 'svelte'
  import { style, active } from '$lib/style'

  export let id = ''
  export let fg = '--clr-winter-morning'
  export let bg = '--clr-cold-winds'
  export let contrast = '--clr-almost-black'

  onMount(() => {
    let options = {
      root: null,
      rootMargin: '0px',
      threshold: 0.6
    }

    let observer = new IntersectionObserver((entries: IntersectionObserverEntry[]) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          style.set(`--fg: var(${fg}); --bg: var(${bg}); --contrast: var(${contrast});`)
          active.set(id)
        }
      })
    }, options)

    observer.observe(document.querySelector(`#${id}`))
  })
</script>

<section {id} style={`--fg: var(${fg}); --bg: var(${bg}); --contrast: var(${contrast});`}>
  <slot />
</section>

<style lang="scss">
  section {
    min-height: 100vh;
    padding: 5rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    background: var(--bg);
    color: var(--fg);
  }

  @media screen and (max-width: 540px) {
    section {
      padding: 2rem;
    }
  }
</style>
