<template>
  <div class="container">
    <div class="mail-box">
      <vsidebar :messages="messages"></vsidebar>
      <vcontent :messages="messages"></vcontent>
    </div>
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar.vue";
import Content from "./components/Content.vue";
import messages from "./data/messages";
import randomMessages from "./data/random-messages";
import { eventBus } from "./main";

export default {
  data() {
    return {
      messages: messages
    };
  },
  created() {
    eventBus.$on("refreshMessages", () => {
      let randomIndex = Math.floor(Math.random() * randomMessages.length);
      let temp = [randomMessages[randomIndex]];
      this.messages = temp.concat(this.messages.slice(0));
    });
    eventBus.$on("sentMessage", (data) => {
      let temp = [data.message];
      this.messages = temp.concat(this.messages.slice(0));
    });
  },
  components: {
    vsidebar: Sidebar,
    vcontent: Content
  }
};
</script>