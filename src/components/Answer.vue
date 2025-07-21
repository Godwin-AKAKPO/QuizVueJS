<template>
    <label :for="id" :class="classes">
        <input :disabled="disabled"  type="radio" name="answer" :id="id" :value="value" 
        @change="onChange" v-model="model">
        {{ value }}
    </label>
</template>

<script setup>
    import {computed} from "vue";
    const props = defineProps({
        id: String,
        disabled : Boolean,
        value : String,
        correctAnswer : String
    })
    const emits = defineEmits(['change'])
    const onChange = (event) => {
        emits('change', event)
    }
    const model = defineModel()
    const classes = computed(() =>({
        disabled : props.disabled,
        right: props.disabled && props.value === props.correctAnswer,
        wrong : props.disabled && props.value !== props.correctAnswer && model.value === props.value
    }))
</script>

<style>

    .disabled{
        opacity: 0.5;
    }
    .right{
        color: green;
        opacity: 1.2;
    }
    .wrong{
        color: red;
        opacity: 1.2;
    }
</style>