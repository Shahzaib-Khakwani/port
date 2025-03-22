<script>
    import { T, useTask } from "@threlte/core";
    
    const radius = 1;      // Base radius
    const height = 1.5;    // Height of pyramid
    const radialSegments = 4;    // 4 sides for pyramid shape
    const heightSegments = 8;    // More segments for smoothness
    
    let rotation = $state({ x: 0, y: 0 });
    
    useTask((delta) => {
        rotation.x += delta;
        rotation.y += delta;
    });
</script>

<T.PerspectiveCamera
    makeDefault
    position={[2, 2, 5]}
/>

<T.AmbientLight intensity={0.5} />
<T.DirectionalLight 
    position={[5, 5, 5]}
    intensity={1}
/>

<T.Mesh 
    position={[0, 3, 0]}
    
>
    <T.ConeGeometry 
        args={[radius, height, radialSegments, heightSegments, false]}
    />
    <T.MeshStandardMaterial 
        color="#4169E1"
        roughness={0.3}    
        metalness={0.1}
    />
</T.Mesh>