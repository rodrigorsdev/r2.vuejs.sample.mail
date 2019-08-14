<template>
  <div class="inbox-body">
    <div class="mail-option">
      <div class="btn-group">
        <a href="#" class="btn" @click="refresh">
          <i class="fa fa-refresh"></i>&nbsp; Refresh
        </a>
      </div>
    </div>
    <vmessages :messages="incomingMessages"></vmessages>
  </div>
</template>

<script>
import Messages from "./Messages.vue";
import { eventBus } from "../main";

export default {
  components: {
    vmessages: Messages
  },
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  computed: {
    incomingMessages() {
      return this.data.messages.filter(function(message) {
        return message.type == "incoming" && !message.isDeleted;
      });
    }
  },
  methods: {
    refresh() {
      eventBus.$emit("refreshMessages");
    }
  }
};
</script>