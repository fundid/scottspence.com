<script lang="ts">
  import { scale_and_fade, viewport } from '$lib/utils'
  import ButtButt from '$lib/images/buttbutt.png'

  export let height = '100px'
  export let width = '160px'
  const puns: string[] = [
    `Ok, well, now that's behind you maybe you'd like to share this?`,
    `Is that two cheeky for you?!`,
    `I know, what a half-arsed attempt at humour!`,
    `I've got some cheek making that crack!`,
    `Cool! You can leave that in the Rear-view now!`,
    `Like it? You can always take another crack at it?`,
    `Butt wait, there's more!`,
    `I'll understand if you think it didn't Butt the mustard!`,
    `Personally, I feel like this is a really half-assed attempt at humour.`,
    `Sorry if I'm being a smart ass.`,
    `Hope this isn't crack-ing you up?`,
    `Ok time to get stuck into the backend again instead of wasting my time writing bottom-drawer jokes.`,
    `I'm a little Behind on my jokes butt a well-Rounded Butt pun always beats a Crappy one.`,
  ]

  const puns_copy = puns.slice()

  let pun: string | null = null

  const random_pun = (): string => {
    if (puns_copy.length === 0) {
      puns_copy.push(pun as string)
      pun = null
    }
    const index = Math.floor(Math.random() * puns_copy.length)
    const new_pun = puns_copy[index]
    puns_copy.splice(index, 1)
    if (pun) {
      puns_copy.push(pun)
    }
    pun = new_pun
    return new_pun
  }

  $: pun = random_pun()

  let intersecting = false
</script>

<div
  use:viewport
  on:enterViewport={() => (intersecting = true)}
  on:exitViewport={() => (intersecting = false)}
>
  <aside class="mb-12 text-center all-prose">
    <p class="mb-6">
      Looks like you have reached the bottom of this page!
    </p>
    {#if intersecting}
      <div class="flex justify-center mb-12">
        <img
          src={ButtButt}
          alt="a cheeky butt"
          {height}
          {width}
          class="h-full"
          transition:scale_and_fade={{ delay: 200, duration: 400 }}
        />
      </div>
    {/if}
    <p class="mb-6">Bummer!</p>
    <p class="mb-6">{pun}</p>
    <button class="btn btn-xs" on:click={random_pun}>
      pun me up
    </button>
  </aside>
</div>
