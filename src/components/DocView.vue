<template lang="pug">
  div.view
    div
      section-def
        dt(slot="title" v-html="doc.title")
        dd(slot="desc" v-html="doc.desc")
    slot(name="documentation" class='documentation-section')
    section
      section-header Examples
      slot
    section(v-if="doc.props || doc.slots || doc.events || doc.functional")
      section-header API
      v-tabs
        v-tab-item(slot="activators" href="#props" ripple v-if="doc.props") Props
        v-tab-item(slot="activators" ripple href="#slots" v-if="doc.slots") Slots
        v-tab-item(slot="activators" ripple href="#functional" v-if="doc.functional") Functional
        v-tab-item(slot="activators" ripple href="#events" v-if="doc.events") Events
        v-tab-content(id="props" slot="content" v-if="doc.props")
          v-card
            v-card-text
              component-parameters(v-bind:params="doc.props", v-bind:headers="propHeaders")
        v-tab-content(id="slots" slot="content" v-if="doc.slots")
          v-card
            v-card-text
              component-parameters(v-bind:params="doc.slots", v-bind:headers="slotHeaders")
        v-tab-content(id="functional" slot="content" v-if="doc.functional")
          v-card
            v-card-text
              component-parameters(v-bind:params="doc.functional" v-bind:headers="functionalHeaders")
        v-tab-content(id="events" slot="content" v-if="doc.events")
          v-card
            v-card-text
              component-parameters(v-bind:params="doc.events" v-bind:headers="eventHeaders")
    slot(name="end")
</template>

<script>
  export default {
    data () {
      return {
        propHeaders: ['Option', 'Type(s)', 'Default', 'Description'],
        slotHeaders: ['Name', 'Description'],
        functionalHeaders: ['Name', 'Class'],
        eventHeaders: ['Name', 'Type(s)', 'Description'],
      }
    },

    props: ['doc']
  }
</script>

<style lang="stylus">
  @import '../stylus/settings/_variables'

  .view
    margin-bottom: 3rem
    max-width: 1024px

  .version
    margin-top: -1rem
    margin-bottom: 1rem
    text-align: right

  .chip--component
    margin-right: 1rem

  dt
    font-weight 900

  .section-text
    line-height: $line-height-root * 1.5
</style>
