<script setup lang="ts">
import { VPTeamPage, VPTeamPageTitle, VPHomeContent } from 'vitepress/theme'
import AMWTeamMembers from './AMWTeamMembers.vue'
import { useData } from '../composables/data'

const { frontmatter: fm } = useData()
</script>

<template>
  <div class="AMWTeam">
    <slot name="team-top" />
    <VPTeamPage>
      <VPTeamPageTitle>
        <template v-if="fm.longtitle" #title> {{ fm.longtitle }} </template>
        <template v-if="fm.introtext" #lead>{{ fm.introtext }}</template>
      </VPTeamPageTitle>
      <AMWTeamMembers :members="fm.members" />
      <VPHomeContent>
        <Content />
      </VPHomeContent>
    </VPTeamPage>
    <slot name="team-bottom" />
  </div>
</template>

<style scoped>
.VPTeamPage {
  margin: 96px 0;
}

@media (min-width: 768px) {
  .VPTeamPage {
    margin: 128px 0;
  }
}
</style>
