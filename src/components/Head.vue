<template>
  <div>
    <b-navbar toggleable="md" type="dark" class="align-center navBar">
      <b-container>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse is-nav id="nav-collapse">
          <b-navbar-nav class="text-left">
            <b-nav-item :to="{ name: 'Menu' }" exact
              ><strong>{{ $t("header.nav-menu") }}</strong>
            </b-nav-item>
            <b-nav-item :to="{ name: 'Pokepedia' }"
              ><strong>Pokepedia</strong>
            </b-nav-item>
            <b-nav-item :to="{ name: 'History' }" v-if="isSessionOn"
              ><strong>{{ $t("header.nav-history") }}</strong>
            </b-nav-item>
            <!-- dropdown to change the $i18n.locale tag -->
            <b-nav-item-dropdown
              v-bind:text="this.$i18n.locale"
              class="text-lowercase"
              right
            >
              <b-dropdown-item href="#" @click="setLocale('en')"
                >ENGLISH</b-dropdown-item
              >
              <b-dropdown-item href="#" @click="setLocale('es')"
                >ESPAÑOL</b-dropdown-item
              >
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
        <Login></Login>
      </b-container>
    </b-navbar>
  </div>
</template>
<script>
import Login from "@/components/Login.vue";
import { mapGetters } from "vuex";

export default {
  components: {
    Login,
  },
  computed: {
    ...mapGetters({ isSessionOn: "userStore/isSessionOn" }),
  },
  methods: {
    setLocale(locale) {
      this.$i18n.locale = locale;
    },
  },
};
</script>

<style scoped>
.navBar {
  background-color: #FD3D30;
}
</style>
