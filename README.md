# Vue3 phone prefix select component
Vue3 phone prefix select component with country name and emoji flag.

## How to

```js
<script>
  import PrefixSelect from '@/components/form/prefix/PrefixSelect.vue'
  
  const prefix_selected = ref(48)
</script>

<template>  
  <PrefixSelect label="Prefix code" v-model="prefix_selected" name="prefix" />
  
  <p> Prefix: {{ prefix_selected }}
</template>
```

## Select image

<img src="https://raw.githubusercontent.com/atomjoy/vue3-phone-prefix-select/main/vue3-phone-prefix.png" width="100%">
