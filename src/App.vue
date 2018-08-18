<template>
  <div id="app">
    Testando
    <content-wrapper class="section fullwidth row" content-class="narrow column" :content-style="{
      backgroundColor: 'red'
    }">
      <img alt="Vue logo" src="./assets/logo.png">
    </content-wrapper>
  </div>
</template>

<script>
import ContentWrapper from './ContentWrapper';

export default {
  name: 'app',
  components: {
    ContentWrapper
  }
}
</script>

<style>
.section {
  background: grey;
}
.fullwidth {
  width: 100vw;
}
.row, .column {
  display: flex;
}
.row {
  flex-direction: row;
}
.column {
  flex-direction: column;
}
.narrow {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}
</style>
