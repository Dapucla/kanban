<template>
  <div :class="dark">
    <header>
      <div class="header-wrap container">
        <div class="header__logo">
          <h1>Канбан</h1>
        </div>
        <!-- /.header__logo -->
        <div class="header__theme">
          <span>Ночная тема</span>
          <toggle-button
            v-model="theme"
            @change="changeTheme();"
            :value="false"
            :labels="{checked: 'Вкл', unchecked: 'Выкл'}"
            :width="70"
            :height="33"
            :color="{checked: '#43d8c9', unchecked: '#43d8c9'}"
            :font-size="10"
          />
        </div>
        <!-- /.header__theme -->
      </div>
    </header>
    <main>
      <add-card></add-card>
      <work-board></work-board>
    </main>
    <modal-name></modal-name>
    <modal-edit
      v-bind:description="description"
      v-bind:date="date"
      v-bind:name="name"
      v-bind:status="status"
      v-bind:date_end="date_end"
    ></modal-edit>
  </div>
</template>
<script>
import taskCard from "./Card.vue";
import addCard from "./AddCard.vue";
import WorkBoard from "./WorkBoard.vue";
import ModalName from "./ModalName.vue";
import ModalEdit from "./ModalEdit.vue";
import draggable from "vuedraggable";
export default {
  data() {
    return {
      theme: false,
      dark: ""
    };
  },
  methods: {
    changeTheme: function(e) {
      this.$store.state.theme = this.theme;
      this.$store.state.dark = "";
      this.$store.state.dark_card = "";
      this.dark = "";
      if (this.theme) {
        this.dark = "dark";
        this.$store.state.dark = "dark";
        this.$store.state.dark_card = "work-card__dark";
      }
    }
  },
  computed: {
    description() {
      return this.$store.state.edit.description;
    },
    date() {
      return this.$store.state.edit.date;
    },
    name() {
      return this.$store.state.edit.name;
    },
    status() {
      return this.$store.state.edit.status;
    },
    date_end() {
      return this.$store.state.edit.date_end;
    }
  },
  components: {
    taskCard: taskCard,
    addCard: addCard,
    WorkBoard: WorkBoard,
    ModalName: ModalName,
    ModalEdit: ModalEdit
  }
};
</script>
<style lang="sass">
@import '../sass/style.sass'
.dark
  z-index: 50
  background-color: #24292E
</style>

