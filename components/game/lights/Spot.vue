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
      this.light = new THREE.SpotLight(0xffffff, 0.4, 10, Math.PI * 0.3)
      this.light.castShadow = true
      this.light.position.set(0, 2, 2)
      this.scene.add(this.light)
      this.scene.add(this.light.target)
    }
  }
}

</script>