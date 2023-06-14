<script lang='ts'>
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()

  let dropzone: HTMLDivElement

  // prevent default to allow drop
  addEventListener('dragenter', (event) => event.preventDefault())

  // prevent default to allow drop
  addEventListener("dragover", (event) => event.preventDefault())

  addEventListener('drop', (event) => {
    event.preventDefault()

    const reader = new FileReader()

    reader.addEventListener('load', (event) => {
      dispatch('drop', event.target.result as string)
    })

    reader.readAsBinaryString((event as any).dataTransfer.files[0])
  })


</script>

<div bind:this={dropzone} />

<style>
  div {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    pointer-events: none;
  }
</style>