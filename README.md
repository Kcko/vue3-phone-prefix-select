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

## Custom prefix select

## How to

```vue
<script setup>
  import CustomPrefixSelect from '@/components/form/prefix/CustomPrefixSelect.vue'
  
  const prefix_selected = ref(48)
  
  function onSubmit(e) {
    let data = new FormData(e.target);    
    for (var pair of data.entries()) {
      console.log("Key:", pair[0], "Value:", pair[1]);
    }
    // axios request here send to server
  }
</sctipt>
<template>
  {{ prefix_selected }}
  
  <form @submit.prevent="onSubmit">
  
    <CustomPrefixSelect label="Prefix" v-model="prefix_selected" name="prefix" />
    
    <button> Send </button>
  </form>
</template>
```

## Custom select image

<img src="https://raw.githubusercontent.com/atomjoy/vue3-phone-prefix-select/main/vue3-phone-prefix-custom.png" width="100%">
