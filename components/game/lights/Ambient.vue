<!-- The Ambient Light -->
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
      this.light = new THREE.AmbientLight(0xffffff, 0.5)
      this.scene.add(this.light)
    }
  }
}

</script>