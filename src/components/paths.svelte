<script lang='ts'>
  import * as THREE from 'three'
  import { T, useThrelte, extend } from '@threlte/core'
  import Dropzone from './dropzone.svelte'
  import { GridHelper } from 'trzy'
  import { MapControls } from 'three/examples/jsm/controls/MapControls'
  import { Line2 } from 'three/addons/lines/Line2.js'
  import { LineMaterial } from 'three/addons/lines/LineMaterial.js'
  import { LineGeometry } from 'three/addons/lines/LineGeometry.js'

  extend({ MapControls })

  const { scene, camera, renderer } = useThrelte()

  let line: THREE.Line | undefined

  const grid = new GridHelper()
  grid.color = new THREE.Color('#aaa')
  grid.rotateX(Math.PI / 2)
  scene.add(grid)

  const handleDrop = (event: CustomEvent<string>) => {
    let path: number[] = []
  
    for (const line of event.detail.split('\n')) {
      const [a, b] = line.split(',')
      const x = Number.parseFloat(a) / 1000
      const y = Number.parseFloat(b) / 1000
      path.push(x, y, 0)
    }

    const vertices = new Float32Array(path)
  
    // const geometry = new THREE.BufferGeometry()
    // geometry.setAttribute('position', new THREE.BufferAttribute(vertices, 3))

    // const material = new THREE.LineBasicMaterial({ color: 'red' })
    // line = new THREE.Line( geometry, material )

    const geometry = new LineGeometry();
    geometry.setPositions( vertices );

    const material = new LineMaterial( {
      color: 'red',
      linewidth: 0.005,
      dashed: false,
      alphaToCoverage: true,
    } );

    line = new Line2( geometry, material );
    line.computeLineDistances();
  }
</script>

<Dropzone on:drop={handleDrop} />

<T.OrthographicCamera
  let:ref
  makeDefault
  position={[0, 0, 0.1]}
  zoom={100}
>
  <T.MapControls
    args={[ref, renderer.domElement]}
    screenSpacePanning={true}
    enableRotate={false}
  />
</T.OrthographicCamera>



<!-- <T is={grid} /> -->

{#if line}
  <T is={line} />
{/if}
