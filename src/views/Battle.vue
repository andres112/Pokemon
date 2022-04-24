<template>
  <div id="app" class="container-fluid">
    <Tittle msg="Pokemon Battle Arena" />
    <Battle></Battle>
  </div>
</template>

<script>
import Tittle from "@/components/Tittle.vue"
import Battle from "@/components/Battle.vue"

import { mapState } from "vuex"

export default {
  name: "BattleView",
  components: {
    Tittle,
    Battle,
  },
  computed: {
    ...mapState({
      players: (state) => state.battle.players,
    }),
  },
  beforeMount() {
    if (this.players.length == 0) {
      this.$router.push({ path: "/" })
    }
  },
}
</script>
