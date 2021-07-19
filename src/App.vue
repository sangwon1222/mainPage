<template>
  <div id="app">
    <topMenu @gameListOn="showGameList" />

    <component
      :is="currentPage"
      :ref="currentPage"
      @gameListOn="showGameList"
    />

    <bottomMenu />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import homePage from "@/pages/home.vue";
import topMenu from "@/components/topMenu.vue";
import bottomMenu from "@/components/bottomMenu.vue";

@Component({
  components: {
    homePage,
    topMenu,
    bottomMenu,
  },
})
export default class App extends Vue {
  private currentPage = "homePage";
  private backupY: number;
  async mounted() {
    //
  }
  showGameList(flag: boolean) {
    if (!(this.$refs.homePage as any)) {
      return;
    }
    if (flag) {
      (this.$refs.homePage as any).gameListFlag = flag;
      this.backupY = window.pageYOffset;
      window.setTimeout(function() {
        window.scrollTo(0, 0);
      }, 500);
    } else {
      (this.$refs.homePage as any).gameListFlag = flag;
      window.scrollTo(0, this.backupY);
    }
  }
}
</script>

<style lang="scss">
#app {
  position: relative;
  overflow: hidden;
  padding: 6rem 0 14rem;
  min-height: 600px;
}
::-webkit-scrollbar {
  display: none;
}
</style>
