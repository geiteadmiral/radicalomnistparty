<script lang="ts">
    import * as Threlte from '@threlte/core'
    import * as Extra from '@threlte/extras'

    

  </script>
  
  <div class="scene">
    <Threlte.Canvas>

      <Threlte.PerspectiveCamera position={{ x: 5, y: 5, z: 5 }} fov={15}>
        <Threlte.OrbitControls autoRotate enableZoom={false} enablePan={false} />
      </Threlte.PerspectiveCamera>
  
      <Threlte.AmbientLight color="white" intensity={0.5} />
  
      <Threlte.DirectionalLight
        color="white"
        intensity={3}
        position={{ x: 10, y: 10 }}
        shadow={{
          camera: { top: 8 },
        }}
      />
  


    <Extra.GLTF url="platypus.glb"  />
    </Threlte.Canvas>
  </div>
  
  <style>
    .scene {
        height: 100vh;
        width: 30vw;
    }
  </style>

  