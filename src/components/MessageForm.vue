<template>
  <div class="message-form ld-over">
    <small class="text-muted">@{{ user.username }}</small>
    <b-form
      class="ld-over"
      :class="{ running: sending }"
      @submit.prevent="onSubmit"
    >
      <div class="ld ld-ring ld-spin" />
      <b-alert
        variant="danger"
        :show="hasError"
      >
        {{ error }}
      </b-alert>
      <b-form-group>
        <b-form-input
          id="message-input"
          v-model="message"
          type="text"
          placeholder="Enter Message"
          autocomplete="off"
          required
          @input="isTyping"
        />
      </b-form-group>
      <div class="clearfix">
        <b-button
          type="submit"
          variant="primary"
          class="float-right"
        >
          Send
        </b-button>
      </div>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapState, mapGetters } from 'vuex'
import { isTyping } from '../chatkit.js'

export default {
  name: 'MessageForm',
  data() {
    return {
      message: ''
    }
  },
  computed: {
    ...mapState([
      'user',
      'sending',
      'error',
      'activeRoom'
    ]),
    ...mapGetters([
      'hasError'
    ])
  },
  methods: {
    ...mapActions([
      'sendMessage',
    ]),
    async onSubmit() {
      const result = await this.sendMessage(this.message)
      if(result) {
        this.message = ''
      }
    },
    async isTyping() {
      await isTyping(this.activeRoom.id)
    }
  }
}
</script>