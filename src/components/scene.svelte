<script lang='ts'>
  import { T, useThrelte } from '@threlte/core'
  import Paths from './paths.svelte'
  import Inspector from 'three-inspect'

  const { scene, camera, renderer } = useThrelte()

  console.log('hi')

  // scene.add(camera.current)

  // new Inspector({
  //   scene,
  //   camera: camera.current as THREE.PerspectiveCamera,
  //   renderer
  // })
</script>

<Paths />

<T.AmbientLight />