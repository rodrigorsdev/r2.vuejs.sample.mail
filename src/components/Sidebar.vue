<template>
  <aside class="sm-side">
    <div class="user-head">
      <img src="src/assets/images/profile.jpg" />
      <div class="user-name">
        <h5>Rodrigo Oliveira</h5>
        <span class="email-address">rodrigo.soliveira2322@gmail.com</span>
      </div>
    </div>

    <div class="compose-wrapper">
      <vcompose></vcompose>
    </div>

    <ul class="inbox-nav">
      <li :class="{active: activeView == vinbox}">
        <a href="#" @click.prevent="navigate('vinbox', 'Inbox')">
          <i class="fa fa-inbox"></i> Inbox
          <span class="label label-danger pull-right">{{unreadMessages.length}}</span>
        </a>
      </li>
      <li :class="{active: activeView == vsent}">
        <a href="#" @click.prevent="navigate('vsent', 'Sent')">
          <i class="fa fa-envelope-o"></i> Sent
          <span class="label label-default pull-right">{{sentMessages.length}}</span>
        </a>
      </li>
      <li :class="{active: activeView == vimportant}">
        <a href="#" @click.prevent="navigate('vimportant', 'Important')">
          <i class="fa fa-bookmark-o"></i> Important
          <span class="label label-warning pull-right">{{importantMessages.length}}</span>
        </a>
      </li>
      <li :class="{active: activeView == vtrash}">
        <a href="#" @click.prevent="navigate('vtrash', 'Trash')">
          <i class="fa fa-trash-o"></i> Trash
          <span class="label label-default pull-right">{{trashedMessages.length}}</span>
        </a>
      </li>
    </ul>
  </aside>
</template>

<script>
import { eventBus } from "../main";
import Conpose from "./Compose.vue";

export default {
  props: {
    messages: {
      type: Array,
      required: true
    }
  },
  created() {
    eventBus.$on("changeView", data => {
      this.activeView = data.tag;
    });
  },
  data() {
    return {
      activeView: "vinbox"
    };
  },
  methods: {
    navigate(newView, title) {
      eventBus.$emit("changeView", {
        tag: newView,
        title: title
      });
    }
  },
  computed: {
    unreadMessages() {
      return this.messages.filter(function(message) {
        return (
          message.type == "incoming" && !message.isRead && !message.isDeleted
        );
      });
    },
    sentMessages() {
      return this.messages.filter(function(message) {
        return message.type == "outgoing" && !message.isDeleted;
      });
    },
    importantMessages() {
      return this.messages.filter(function(message) {
        return (
          message.type == "incoming" &&
          message.isImportant &&
          !message.isDeleted
        );
      });
    },
    trashedMessages() {
      return this.messages.filter(function(message) {
        return message.isDeleted;
      });
    }
  },
  components: {
    vcompose: Conpose
  }
};
</script>