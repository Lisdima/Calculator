<template>
  <div class="hello" @click="test">Hello world</div>
</template>

<script>
export default {
  methods: {
    test() {
      console.log('Логика работает');
    }
  }
}
</script>
