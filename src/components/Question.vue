<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in question.choices" :key="choice"> 
                <label :for="`answer${index}`">
                    <input  type="radio" name="answer" :id="`answer${index}`" :value="choice" v-model="answer">
                    {{ choice }}
                </label>
            </li>
        </ul>

        <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>
    </div>
</template>

<script setup>

    import  {ref, computed} from 'vue';

    defineProps({
        question : Object 
    })
    const emits = defineEmits(['answer']);
    const answer = ref(null);
    const hasAnswer = computed(() => answer.value !== null)

</script>

<style>
    .question{
        padding-top: 2rem;
    }
    .question button {
        margin-left: auto;
        display : block;
    }
</style>