<template lang="pug">
  q-drawer(
    show-if-above
    :value="value"
    @input="handleInput"
    v-bind="{bordered, elevated}"
  )
    q-scroll-area.fit.q-pa-sm
      q-list
        template(v-for="(item) in items")
          q-dynamic-item(:item="item" @to="handleTo")
</template>
<script lang="ts">
  import {Component, Prop, Vue} from 'vue-property-decorator'
  import QDynamicItem from './QDynamicItem.vue'
  import {NavItem, NavTo} from './types/navigation'

  @Component({
    components: {
      QDynamicItem,
    },
  })
  export default class Navigation extends Vue {

    @Prop() items: NavItem[]
    @Prop({default: false}) elevated: boolean
    @Prop({default: true}) bordered: boolean
    @Prop() value: boolean

    handleInput(value: boolean) {
      this.$emit('input', value)
    }

    handleTo(to: NavTo) {
      this.$emit('to', to)
    }
  }
</script>
