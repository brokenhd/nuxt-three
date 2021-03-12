<!-- The Game World -->

<template>

  <div class="world">
    <canvas>
      <!-- <GameBox :scene='scene'/> -->
      <GameLights :scene='scene'/>
    </canvas>
  </div>

</template>

<!-- ––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––– -->

<script>
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'

export default {
  data () {
    return {
      scene: null
    }
  },
  mounted () {
    this.loadScene()
  },
  methods: {
    loadScene () {
      const canvas = this.$el.querySelector('canvas')
      this.scene = new THREE.Scene()

      const material = new THREE.MeshStandardMaterial()
      material.roughness = 0.4

      const sphere = new THREE.Mesh(
        new THREE.SphereBufferGeometry(0.5, 64, 64),
        material
      )
      sphere.castShadow = true

      const plane = new THREE.Mesh(
        new THREE.PlaneBufferGeometry(5, 5),
        material
      )
      plane.position.y = -0.5
      plane.rotation.x = Math.PI * -0.5
      plane.receiveShadow = true

      this.scene.add(sphere, plane)

      // Sizes
      const sizes = {
        width: window.innerWidth,
        height: window.innerHeight
      }

      window.addEventListener('resize', () => {
        sizes.width = window.innerWidth
        sizes.height = window.innerHeight

        // Update Camera
        camera.aspect = sizes.width / sizes.height
        camera.updateProjectionMatrix()
        renderer.setSize(sizes.width, sizes.height)
      })

      // Camera
      const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height)
      camera.position.z = 3
      camera.lookAt(sphere.position)
      this.scene.add(camera)

      // Controls
      const controls = new OrbitControls(camera, canvas)
      controls.enableDamping = true

      // Renderer
      const renderer = new THREE.WebGLRenderer({
        canvas: canvas
      })
      renderer.setSize(sizes.width, sizes.height)
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
      renderer.shadowMap.enabled = true

      // Clock
      const clock = new THREE.Clock()

      // Animations
      const tick = () => {
        // Clock
        const elapsedTime = clock.getElapsedTime()

        // Update Controls
        controls.update()

        // Render
        renderer.render(this.scene, camera)
        window.requestAnimationFrame(tick)
      }

      tick()
    }
  }
}

</script>

<!-- ––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––––– -->

<style lang='stylus' scoped>

canvas
  position fixed
  top 0
  left 0
  width 100%
  height 100%
  outline none

</style>