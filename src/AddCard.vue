<template>
  <div class="add-card container">
    <span>Добавить задачу</span>
    <div class="add-card__field">
      <input v-model="description" type="text" placeholder="Задача" />
      <button v-on:click="createCard($event)">+</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      description: "",
      card: null
    };
  },
  methods: {
    createCard: function(event) {
      this.$store.commit("increment");
      this.$store.state.cards.push({
        id: this.$store.state.count,
        status: "plan",
        description: this.description,
        date: "",
        date_end: "",
        name: this.$store.state.name
      });
      event.preventDefault();
      this.description = "";
    }
  }
};
</script>