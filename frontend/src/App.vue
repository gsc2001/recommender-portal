<template>
    <v-app color="#EDEBD7">
        <Navbar :current="$route.name" />
        <v-main>
            <v-content>
                <v-overlay :value="overlay">
                     <v-progress-circular
                        color="#4e4d5c"
                        size="100"
                        width="10"
                        indeterminate
                    >
                        <v-icon class="mdi-spin mdi-48px" color="#4e4d5c">mdi-lock-reset</v-icon>
                    </v-progress-circular>
                </v-overlay>
                <router-view />
                <AddItem :currPage="$route.name" />
            </v-content>
        </v-main>
    </v-app>
</template>

<script>
import Navbar from '@/components/Navbar'
import AddItem from '@/components/AddItem'
import { mapState } from 'vuex'
export default {
  name: 'App',
  props: {
    source: String
  },
  components: {
    Navbar,
    AddItem
  },
  data: () => ({
    drawer: null,
    sheet: false,
    stepNum: 1,
    currPage: 'Home',
    current: 'Home'
  }),
  computed: mapState({
    overlay: state => state.loading
  }),
  methods: {
    closeSheet: function () {
      this.sheet = false
    },
    openSheet: function (sheetType) {
      this.stepNum = 1
      this.sheetType = sheetType
      this.sheet = true
    },
    changeCurrPage: function (newCurrPage) {
      this.currPage = newCurrPage
    }
  }
}
</script>
