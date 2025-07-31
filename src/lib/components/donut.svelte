<script>
    import { T, useTask} from '@threlte/core'
    import { interactivity, useTexture, useGltf, useDraco} from '@threlte/extras'
    import { Spring } from 'svelte/motion'
    import { derived } from 'svelte/store'

    
    interactivity()

    let rotation = $state(0)
    let pos = $state(0)
    useTask((delta) => {
        rotation += delta * 0.2
        pos += delta * 0.2
    })

    const dracoLoader = useDraco()

    const gltf = useGltf('/assets/crisps.gltf', {
        dracoLoader
    })
    const banana_gltf = useGltf('/assets/banana.gltf', {
        dracoLoader
    })
    
    // let bananaNodes = $derived($banana_gltf?.nodes)

    const bananaNodes = derived(banana_gltf, ($banana_gltf) => {
        if (!$banana_gltf || !$banana_gltf.nodes) return []
        return Object.entries($banana_gltf.nodes)
        .filter(([_, node]) => node.isMesh && node.geometry)
    })

    const texture = useTexture('/textures/4.png')
    const btexture = useTexture('/textures/7.png')

    const list = [...Array(150)].map((value, index) => ({
        index: index,
        position: [
            (Math.random() - 0.5) * 10,
            (Math.random() - 0.5) * 10,
            (Math.random() - 0.5) * 10
        ],
        scale: 0.8 + Math.random() * 0.8,
        rotation:[
            Math.random() * Math.PI,
            Math.random() * Math.PI,
            0
        ],
        scaleSpring: new Spring(1)
    }))

</script>

{#if $gltf && bananaNodes}
    {#await texture then map}
        {#await btexture then bmap}
            {#each list as obj}
                {#if obj.index % 2 === 0}
                    <!-- Crisp bag -->
                    <T.Mesh
                    key={"crisp-" + obj.index}
                    position={[obj.position[0], obj.position[1] + Math.sin(pos), obj.position[2] + Math.cos(pos)]}
                    rotation={[obj.rotation[0], rotation + obj.rotation[1], obj.rotation[2]]}
                    scale={obj.scale * obj.scaleSpring.current}
                    onpointerenter={() => (obj.scaleSpring.target = 1.5)}
                    onpointerleave={() => (obj.scaleSpring.target = 1)}
                    geometry={$gltf.nodes['bagFlat'].geometry}
                    >
                    <T.MeshMatcapMaterial matcap={map} />
                    </T.Mesh>
                {:else}
                    <!-- Banana parts (each part of the model) -->
                    {#each $bananaNodes as [key, node]}
                    <T.Mesh
                        key={"banana-" + obj.index + "-" + key}
                        position={[obj.position[0], obj.position[1] + Math.sin(pos), obj.position[2] + Math.cos(pos)]}
                        rotation={[obj.rotation[0], rotation + obj.rotation[1], obj.rotation[2]]}
                        scale={obj.scale * obj.scaleSpring.current}
                        onpointerenter={() => (obj.scaleSpring.target = 1.5)}
                        onpointerleave={() => (obj.scaleSpring.target = 1)}
                        geometry={node.geometry}
                    >
                        <T.MeshMatcapMaterial matcap={bmap} />
                    </T.Mesh>
                    {/each}
                {/if}
            {/each}
        {/await}
    {/await}
{/if}