<!-- The Box Object -->
<template></template>

<script>
import * as THREE from 'three'

export default {
  props: ['scene'],
  data () {
    return {
      box: null,
      material: null
    }
  },
  mounted () {
    this.setMaterial()
    this.createBox()
    
    this.box.castShadow = true
    this.scene.add(this.box)
  },
  methods: {
    setMaterial () {
      this.material = new THREE.MeshStandardMaterial()
      this.material.roughness = 0.4
    },

    createBox() {
      this.box = new THREE.Mesh(
        new THREE.BoxBufferGeometry(1, 1, 1),
        this.material
      )
    }
  }
}

</script>