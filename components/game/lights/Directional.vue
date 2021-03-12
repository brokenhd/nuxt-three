<!-- The Spot Light -->
<template></template>

<script>
import * as THREE from 'three'

export default {
  props: [
    'scene',
    'config'
  ],
  data () {
    return {
      light: null
    }
  },
  mounted () {
    this.createLight()
  },
  methods: {
    createLight () {
      this.light = new THREE.DirectionalLight(0x00fffc, 0.3)
      this.light.castShadow = true

      this.light.shadow.mapSize.width = 1024
      this.light.shadow.mapSize.height = 1024
      this.light.shadow.radius = 10
      this.scene.add(this.light)
    }
  }
}

</script>