<!-- The Lights -->
<template>

  <div class="lights">
    <GameLightsAmbient :scene='scene'/>
    <GameLightsDirectional :scene='scene'/>
    <GameLightsSpot :scene='scene'/>
  </div>

</template>

<script>
import * as THREE from 'three'

export default {
  props: ['scene'],
  data () {
    return {
      lights: []
    }
  },
  mounted () {
  },
  methods: {
  }
}

</script>