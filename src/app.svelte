<script lang='ts'>
  import { Canvas } from '@threlte/core'
  import Scene from './components/scene.svelte'
  import Dropzone from './components/dropzone.svelte'
</script>

<Canvas useLegacyLights={false} frameloop={'always'}>
  <Scene />
</Canvas>
<Dropzone />