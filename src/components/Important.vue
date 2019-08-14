<template>
  <div class="inbox-body">
    <vmessages :messages="importantMessages"></vmessages>
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
    importantMessages() {
      return this.data.messages.filter(function(message) {
        return (
          message.type == "incoming" &&
          message.isImportant &&
          !message.isDeleted
        );
      });
    }
  },
  components: {
    vmessages: Messages
  }
};
</script>