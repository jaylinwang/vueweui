<template>
<div>
  <v-progress :percent="30">
  </v-progress>
  <v-progress :percent="40" status="active">
  </v-progress>
  <v-progress :percent="60" status="exception">
  </v-progress>
  <v-progress :percent="100">
  </v-progress>
  <v-progress :percent="60" hide-info>
  </v-progress>
</div>
</template>

<script>
export default {

}
</script>
