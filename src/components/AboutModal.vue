<template>
  <q-modal
    ref="modal"
    @escape-key="close()"
  >
    <div class="modal-header">
      <img id="logo" src="statics/icon.png"/>
      <h4>{{ name }}</h4>
      <h6>{{ description }}</h6>
    </div>
    <div class="modal-body">
      <p>Built on <a href="https://quasar-framework.org">Quasar Framework</a> by <a :href="'mailto:' + author.email">{{ author.name }}</a></p>
      <p id="version">v{{ version }} - <a :href="'http://en.wikipedia.org/wiki/' + license + '_License'">{{ license }}</a></p>
    </div>
    <div class="modal-buttons row">
      <q-btn
        flat
        @click="close()"
      >Cancel</q-btn>
      <q-btn
        flat
        @click="goToGitHub()"
      >Contribute</q-btn>
    </div>
  </q-modal>
</template>

<script>
import {
  QModal,
  QBtn
} from 'quasar'
import * as INFO from '../../package.json'
import * as LICENSE from '../../LICENSE.txt'

export default {
  name: 'about-modal',
  components: {
    QModal,
    QBtn
  },
  data () {
    return {
      name: INFO.name,
      description: INFO.description,
      version: INFO.version,
      license: INFO.license,
      author: INFO.author,
      licenseContent: LICENSE,
      github: INFO.repository.url.replace(':', '/').replace('.git', '').replace('git@', 'https://')
    }
  },
  methods: {
    open () {
      this.$refs.modal.open()
    },
    close () {
      this.$refs.modal.close()
    },
    toggle () {
      this.$refs.modal.toggle()
    },
    goToGitHub () {
      window.open(this.github)
    }
  }
}
</script>

<style scoped lang="stylus">
@require '../themes/app.variables'

#logo
  display block
  margin 16px auto

  &+h4
    font-family 'LibreBaskerville', serif !important

    &:first-letter
      text-transform capitalize

  &+h4+h6
    color $tertiary
    margin-bottom 1rem

.modal-header, .modal-body
  text-align center
</style>
