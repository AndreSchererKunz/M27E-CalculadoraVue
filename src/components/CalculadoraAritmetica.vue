<script setup>
    import { reactive } from 'vue';

    const estado = reactive({
    primeiroNumero: '',
    segundoNumero: '',
    operacoes: {
    adicao: (a, b) => a + b,
    subtracao: (a, b) => a - b,
    multiplicacao: (a, b) => a * b,
    divisao: (a, b) => (b !== 0 ? a / b : 'Divisao por zero'),
    },
    resultado: 0,
});

const calculaResultado = () => {
    const { primeiroNumero, segundoNumero, operacaoMatematica } = estado;
    const num1 = parseFloat(primeiroNumero);
    const num2 = parseFloat(segundoNumero);
    
    estado.resultado = !isNaN(num1) && !isNaN(num2) ? estado.operacoes[operacaoMatematica](num1, num2) : 'Entrada inválida';
};
</script>

<template>
    <div class="container">
        <h1 class="p-5 mb-4 mt-4 bg-light rounded-3 text-center">Calculadora Aritmética</h1>

        <select class="mt-3 mb-1" v-model="estado.operacaoMatematica" @change="calculaResultado">
            <option value="adicao">Adição</option>
            <option value="subtracao">Subtração</option>
            <option value="multiplicacao">Multiplicação</option>
            <option value="divisao">Divisão</option>
        </select>

        <input class="form-control mt-3 mb-3" type="text" v-model="estado.primeiroNumero" @input="calculaResultado" />
        <input class="form-control mb-3" type="text" v-model="estado.segundoNumero" @input="calculaResultado" />
        
        <p class="text-decoration-underline">
            Resultado: {{ estado.resultado }}
        </p>
    </div> 
</template>