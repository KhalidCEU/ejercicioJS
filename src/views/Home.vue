<script setup lang="js">
import MainBox from '@/components/MainBox.vue';
import { ref } from 'vue';

const wordCount = ref(0);
const password = ref('');

const dictionary = [
  'soil', 'queen', 'fixture', 'waste', 'behead',
  'tank', 'expertise', 'introduce', 'passive', 'cultivate',
  'menu', 'tax', 'sigh', 'fibre', 'beam', 'extraterrestrial',
  'policy', 'trait', 'ego', 'speech', 'clinic', 'pride', 'chain',
  'regard', 'solid', 'matter', 'flatware', 'witness', 'enlarge',
  'cold', 'finish', 'realize', 'midnight', 'displace', 'wound',
  'attention', 'mixture', 'dominate', 'age', 'mask', 'governor'
];

const capitalize = ((word) => {
    const capitalizedWord = word.charAt(0).toUpperCase() + word.slice(1);
    return capitalizedWord;
});

const generatePassword = ((count)=> {
    let generatedPassword = ''

    for (let i = 0; i < count; i++) {
        const index = Math.floor(Math.random() * dictionary.length)
        const word = capitalize(dictionary[index]);
        generatedPassword += word;
    }
    password.value = generatedPassword;
});

const handleGeneratePassword = () => {
    if (wordCount.value > 0) {
        generatePassword(wordCount.value);
    }
};

</script>

<template>
    <div class="flex flex-col min-h-screen">
      <h1 class="text-center text font-semibold text-xl mt-8 mb-6">Generador de contraseñas</h1>
      <div class="flex-grow flex flex-col items-center mt-[30vh]">
        <div class="w-[40%]  ">
            <MainBox
                v-model:word-count="wordCount"
                @generate-password="handleGeneratePassword"
            />
        </div>
        <div v-if="password" class="flex mt-10 flex-col items-center justify-center gap-3">
            <p class="font-medium">Contraseña generada: </p>
            <p>{{password}}</p>
        </div>
      </div>
    </div>
  </template>