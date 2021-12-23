<template>
  <collapsable-card :title="$t('app.general.title.ttyd')" icon="$console" :draggable="true"
    layout-path="dashboard.ttyd-card">
    <template v-slot:menu>
      <app-btn-collapse-group>
        <app-btn
          @click="ReLoadttyd()"
          :elevation="2"
          small
          class="ml-1">
            {{$t('app.ttyd.btn.refresh')}}
        </app-btn>
      </app-btn-collapse-group>
    </template>
    <div>
      <iframe style="width: 100%;" :height="300" id="ttyd-iframe" ref="iframe" :src="Path" ></iframe>
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
  components: {
  }
})

export default class TtydCard extends Mixins(StateMixin) {
  @Prop({
    type: Boolean,
    default: true
  })
  enabled!: boolean

  Path = ''

  get inLayout (): boolean {
    return (this.$store.state.config.layoutMode)
  }

  ReLoadttyd () {
    this.Path = ''
    this.Path = store.state.config?.apiUrl + ':7681?t=' + Date.parse(new Date().toString()).toString()
  }
}
</script>
