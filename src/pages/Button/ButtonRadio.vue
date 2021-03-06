<template>
  <div class="uk-block">
    <h2>Button Radio</h2>
    <hr class="uk-article-divider">
    <!-- DEMO -->
    <vk-button-radio
      :group="props.group.demo.value"
      :value="props.value.demo.value"
      @change="
        events.change.emited = true,
        props.value.demo.value = arguments[0]
      ">
      <vk-button :value="1">Button 1</vk-button>
      <vk-button :value="2">Button 2</vk-button>
      <vk-button :value="3">Button 3</vk-button>
    </vk-button-radio>
    <!-- DESC -->
    <div class="uk-margin-large">
      The <code>vk-button-radio</code> component, acting like a radio form field, allows toggling between a group of <code>vk-button</code> buttons.
    </div>
    <!-- TABS -->
    <vk-tabs
      :index="tabsIndex"
      @change="tabsIndex = arguments[0]">
      <vk-tabs-item name="Props">
        <vk-docs-props
          :props="props"
          @change="props[arguments[0]].demo.value = arguments[1]">
        </vk-docs-props>
      </vk-tabs-item>
      <vk-tabs-item name="Slots">
        <vk-docs-slots :slots="slots"></vk-docs-slots>
      </vk-tabs-item>
      <vk-tabs-item name="Events">
        <vk-docs-events :events="events"></vk-docs-events>
      </vk-tabs-item>
      <vk-tabs-item name="Example">
        <vk-docs-code>{{ code }}</vk-docs-code>
      </vk-tabs-item>
    </vk-tabs>
  </div>
</template>

<script>
import Component from '../../lib/ButtonRadio'
import mixin from '../_mixin'
import { mergeProps } from '../../helpers/pages'

export default {
  name: 'PageButtonRadio',
  mixins: [mixin],
  data: () => ({
    tabsIndex: 0,
    props: mergeProps(Component.props, props),
    slots,
    events,
    example
  })
}

const props = {
  value: {
    description: 'The current value reflecting the selected button one.',
    demo: {
      type: 'Select',
      options: [
        { text: 'default', value: null },
        { text: '1', value: 1 },
        { text: '2', value: 2 },
        { text: '3', value: 3 }
      ],
      value: ''
    }
  },
  group: {
    description: 'Whether to display the buttons grouped together.',
    demo: {
      type: 'Boolean',
      value: true
    }
  }
}

const slots = {
  default: {
    description: 'The list of <code>vk-button</code> components.'
  }
}

const events = {
  change: {
    description: `Emited on the intention to change the selection passing as argument the
      resulting value.`,
    emited: false
  }
}

const example =
`<vk-button-radio {attrs}
  @change="value = arguments[0]">
  <vk-button :value="1">Button 1</vk-button>
  <vk-button :value="2">Button 2</vk-button>
  <vk-button :value="3">Button 3</vk-button>
</vk-button-radio>`
</script>
