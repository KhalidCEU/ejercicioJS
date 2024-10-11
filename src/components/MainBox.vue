<script setup lang="js">
import { ref, watch } from 'vue'
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'
import { vAutoAnimate } from '@formkit/auto-animate/vue'
import { Button } from '@/components/ui/button'
import {
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from '@/components/ui/form'
import { Input } from '@/components/ui/input'

const inputNumber = ref(0);
const emit = defineEmits(['update:wordCount', 'generatePassword']);

const formSchema = toTypedSchema(z.object({
  inputNumber: z.number().min(1).max(10),
}))

const { isFieldDirty, handleSubmit } = useForm({
  validationSchema: formSchema,
})

const onSubmit = handleSubmit((values) => {
    inputNumber.value = values.inputNumber;
    emit('update:wordCount', inputNumber.value);
    emit('generatePassword');
    return false;
})
</script>

<template>
    <form class="space-y-6" @submit.prevent="onSubmit">
        <FormField v-slot="{ componentField }" name="inputNumber" :validate-on-blur="!isFieldDirty">
        <FormItem v-auto-animate>
            <FormLabel>Número de palabras (1 a 10)</FormLabel>
            <FormControl>
            <Input type="number" placeholder="Ej.: 10" v-bind="componentField" />
            </FormControl>
            <FormMessage />
        </FormItem>
        </FormField>
        <Button type="submit">
            Generar contraseña
        </Button>
    </form>
</template>
