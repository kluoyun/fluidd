<template>
  <collapsable-card :title="$t('app.general.title.ttyd')" icon="$files" :draggable="true"
    layout-path="dashboard.ttyd-card">

    <div>
      <iframe style="width: 100%;" :height="300" id="ttyd-iframe" ref="iframe" :src="src" ></iframe>
    </div>
  </collapsable-card>

</template>

<script lang="ts">
import store from '@/store'
import {
  Component,
  Mixins,
  Prop
} from 'vue-property-decorator'
import StateMixin from '@/mixins/state'

@Component({
  components: {}
})

export default class TtydCard extends Mixins(StateMixin) {
  @Prop({
    type: Boolean,
    default: true
  })
  enabled!: boolean

  get inLayout (): boolean {
    return (this.$store.state.config.layoutMode)
  }

  get src () {
    return (store.state.config?.apiUrl + ':7681')
  }
}
</script>
