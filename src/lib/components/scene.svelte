<script>
  import { T, useTask } from '@threlte/core'
  import { Gizmo, interactivity, OrbitControls } from '@threlte/extras'
  import { Spring } from 'svelte/motion'
  import Donut from '$lib/components/donut.svelte'

  interactivity()

  const scale = new Spring(1)

  let rotation = $state(0)
  useTask((delta) => {
    rotation += delta
  })
</script>

<T.Color args={["#FFC800"]} attach={"background"} ></T.Color>

<T.PerspectiveCamera
  makeDefault
  position={[0, 0, 5]}
  fov={45}
  near={0.1}
  far={200}
>
  <!-- <OrbitControls>
  <Gizmo />
  </OrbitControls> -->
</T.PerspectiveCamera>

<T.DirectionalLight
  position.y={10}
  position.z={10}
/>
<T.AmbientLight intensity={0.3} />

<Donut />