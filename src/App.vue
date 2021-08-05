<template>
  <div id="app">
    <main>
      <Name />
      <Name username="Macro" age="33"/>
      <Name username="Sergey" age="29"/>


      <Weather />
    </main>
  </div>
</template>

<script>
import Name from './Name';
import Weather from './Weather';

export default {
  name: 'App',
  components: {Weather, Name},
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@800&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
}

main {

}
</style>
