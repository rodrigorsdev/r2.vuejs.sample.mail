<template>
  <div class="inbox-body">
    <vmessages :messages="trashedMessages"></vmessages>
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
    trashedMessages() {
      return this.data.messages.filter(function(message) {
        return message.isDeleted;
      });
    }
  },
  components: {
    vmessages: Messages
  }
};
</script>