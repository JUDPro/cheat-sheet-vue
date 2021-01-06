<template>
  <div class="some-component">
    <div v-if="typeof(someProps) == 'string'" :title="'Это компонент'">{{someProps}}</div>
    <div :title="'Это компонент'">{{someProps.item}}</div>
  </div>
</template>

<script>
export default {
  name: 'some-component',
  data: () => ({}),
  props: [
    'someProps',
  ],
};
</script>

<style>
.some-component {
  font-size: 20px;
  color: brown;
  margin: 15px;
}
</style>
