<template>
  <section id="name">
    <h1>{{ username || 'Username' }} - {{ age || 'Возраст неизвестен' }}{{ age && ' - ' + date }}</h1>
    <h1 v-show="count">{{ count }}</h1>
    <button @click="getName">Click!</button>
  </section>
</template>

<script>
import moment from 'moment';

export default {
  name: 'Name',
  components: {},

  /* Входные данные с родительского компанента App (тот кто вызывает текущие компонент Name) */
  props: {
    username: String,
    age: Number,
  },

  data: () => ({
    count: 0,
  }),

  computed: {
    date: (self) => {
      return moment().subtract(self.age, 'years').format('MMM YYYY');
    }
  },

  methods: {
    getName() {
      ++this.count
      console.log('Submit name: ' + (this.username || 'Username') + ' ' + this.count);
    }
  },

  watch: {},

  created() {
  },

  mounted() {
  },
}
</script>

<style scoped>
#name {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 40%;
  height: 100px;
  margin: 30px auto;
  border: 3px solid red;
  box-shadow: 5px 3px 8px red;
  color: white;
  border-radius: 0 30px;
}
</style>
