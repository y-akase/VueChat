<template>
  <div class="message-list">
    <h4>Messages</h4>
    <hr>
    <div
      id="chat-messages"
      v-chat-scroll="{smooth: true}"
      class="message-group"
    >
      <div
        v-for="(message, index) in messages"
        :key="index"
        class="message"
      >
        <div class="clearfix">
          <h4 class="message-title">
            {{ message.name }}
          </h4>
          <small class="text-muted float-right">@{{ message.username }}</small>
        </div>
        <p class="message-text">
          {{ message.text }}
        </p>
        <div class="clearfix">
          <small class="text-muted float-right">{{ message.date }}</small>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'MessageList',
  computed: {
    ...mapState([
      'messages',
    ])
  }
}
</script>

<style lang="sass">
.message-list
  padding-right: 15px
  margin-bottom: 15px

.message-group
  height: 65vh !important
  overflow-y: scroll

.message
  padding: 10px
  margin-bottom: 15px
  border: 1px solid lightblue
  border-radius: 4px

.message-title
  display:inline
  font-size: 1rem

.message-text
  margin-bottom: 0
  color: gray

.user-typing
  height: 1rem</style>