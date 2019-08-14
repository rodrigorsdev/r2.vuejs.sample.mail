<template>
  <div class="inbox-body">
    <vmessages :messages="sentMessages"></vmessages>
  </div>
</template>

<script>
import Messages from "./Messages.vue";

export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    sentMessages() {
      return this.data.messages.filter(function(message) {
        return message.type == "outgoing" && !message.isDeleted;
      });
    }
  },
  components: {
    vmessages: Messages
  }
};
</script>