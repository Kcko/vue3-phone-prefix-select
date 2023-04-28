<template>
	<label v-if="label" :for="name">{{ label }}</label>
	<div class="custom-select" @blur="open = false" :tabindex="tabindex">
		<div class="selected" :class="{ open: open, inactive: inactive }" @click="open = !open">{{ selected }} <i class="fas fa-caret-down selected-icon"></i></div>
		<div ref="items" class="items" :class="{ selectHide: !open }">
			<div v-for="o of options" :key="o.prefix" :value="o.prefix" @click="updateClick(o)">{{ o.name }} {{ o.emoji }} +{{ o.prefix }}</div>
		</div>
		<input ref="input" type="hidden" v-model="modelValue" :name="name" />
	</div>
</template>

<script setup>
import { ref, onMounted, toRefs } from 'vue'
import options from './json/country.json'

const emit = defineEmits(['update:modelValue', 'change', 'click', 'blur'])
const props = defineProps({
	label: { type: String },
	name: { type: String },
	modelValue: { type: String },
	tabindex: { type: Number, default: 0 },
})
let { label, name, modelValue, tabindex } = toRefs(props)
const input = ref(null)
const selected = ref(null)
const inactive = ref(false)
const open = ref(false)

function clear() {
	selected.value = `${options[0].emoji}  +${options[0].prefix}`
	modelValue.value = options[0].prefix
	inactive.value = false
}

onMounted(() => {
	if (modelValue.value !== null) {
		let option = options?.find((option) => parseInt(option.prefix) === modelValue.value)
		if (option?.prefix) {
			selected.value = `${option.emoji}  +${option.prefix}`
		} else {
			clear()
		}
	} else {
		clear()
	}
})

function updateClick(option = null) {
	if (option == null) {
		clear()
		open.value = false
	} else {
		modelValue.value = option.prefix ?? null
		selected.value = `${option.emoji}  +${option.prefix}`
		inactive.value = false
		open.value = false
	}
	emit('update:modelValue', modelValue.value)
}
</script>

<style scoped>
.custom-select {
	position: relative;
	float: left;
	width: 100%;
	outline: none;
	padding: 0px;
}
.custom-select .selected {
	font-size: 1rem;
	padding: 1rem 1.5rem;
	box-sizing: border-box;
	background-color: transparent;
	border-radius: 6px;
	border: 1px solid #dfe0ea;
	cursor: pointer;
}
.custom-select .selected.open {
	border: 1px solid #07f;
	background: linear-gradient(#fff, #fff) padding-box, linear-gradient(to right, #07f, darkorchid) border-box;
	border: 1px solid transparent;
}
.custom-select .selected.inactive {
	color: #dfe0ea;
	font-weight: 500;
}
.custom-select .selected .selected-icon {
	color: #dfe0ea;
	position: absolute;
	top: calc(50% - (1rem / 2));
	right: 1.5em;
	transition: all 0.6s;
}
.custom-select .selected.open .selected-icon {
	color: #07f;
	transform: rotate(180deg);
}
.custom-select .items {
	position: absolute;
	top: 4rem;
	left: 0;
	color: #222;
	background-color: #fefefe;
	border: 1px solid #07f;
	border-radius: 10px;
	box-shadow: 0px 9px 9px rgba(0, 0, 0, 0.2);
	z-index: 1;
	max-height: 350px;
	overflow-y: auto;
	padding: 10px;
	box-sizing: border-box;
	scrollbar-width: thin;
	scrollbar-color: #07f #dfe0ea;
}
.custom-select .items::-webkit-scrollbar {
	width: 4px;
	background-color: #dfe0ea;
}
.custom-select .items::-webkit-scrollbar-thumb {
	background: #07f;
}
.custom-select .items div {
	color: #07f;
	padding-left: 1em;
	cursor: pointer;
	user-select: none;
	padding: 1rem 1.5rem;
	transition: all 1s;
}
.custom-select .items div:hover {
	color: #07f;
	background-color: #0075ff33;
}
.custom-select .items .selected-option {
	color: #222;
	background-color: #07f;
}
.selectHide {
	display: none;
}
</style>

<!--
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
  <form @submit.prevent="onSubmit">
    <CustomPrefixSelect label="Prefix" v-model="prefix_selected" name="prefix" />

    <button> Send </button>
  </form>
</template>
-->
