<script>
    import { T, useLoader} from '@threlte/core'
    import { Align, Text3DGeometry, Float, useTexture } from '@threlte/extras'
    import { FontLoader } from 'three/examples/jsm/loaders/FontLoader.js'

    let font = useLoader(FontLoader).load('/fonts/helvetiker_regular.typeface.json')

    const texture = useTexture('/textures/2.png')

    let text = $state("Over a million people live in places where it's easier to buy crisps than fresh fruit")

</script>

{#await texture then map}
    {#if $font}
        <Align>
            {#snippet children({ align})}
            <Float>
                <T.Mesh>
                    <Text3DGeometry 
                        font={$font}
                        text={text}
                        size={0.5}
                        height={0.2}
                        curveSegments={12}
                        bevelEnabled
                        bevelThickness={0.02}
                        bevelSize={0.02}
                        bevelOffset={0}
                        bevelSegments={5}
                        depth={0.01}
                        smoothness={0.5}
                        oncreate={align}
                        />
                    <T.MeshMatcapMaterial 
                    matcap={map}
                    toneMapped={false}
                    metalness={0.1}
                    roughness={0.1}
                    />
                </T.Mesh>
            </Float>
            {/snippet}
        </Align>
    {/if}
{/await}