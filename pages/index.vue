<script setup>
import { ref } from 'vue';

const titulo = ref('Título');
const dado = ref('exemplo');

</script>

<template>

<main>
    <h1>{{ titulo }}</h1>

    <section>
        <article>
            <h2>Seção</h2>
            <p>{{ dado }}</p>
        </article>
        <figure>
            <img src="https://via.placeholder.com/150" alt="Imagem de exemplo">
            <figcaption>legenda da img</figcaption>
        </figure>
    </section>
    
    <section>
        <table>
            <thead>
                <tr>
                    <th>{{ dado }} 1</th>
                    <th>{{ dado }} 2</th>
                    <th>{{ dado }} 3</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Linha 1</td>
                    <td>Linha 1</td>
                    <td>Linha 1</td>
                </tr>
                <tr>
                    <td>Linha 2</td>
                    <td>Linha 2</td>
                    <td>Linha 2</td>
                </tr>
                <tr>
                    <td>Linha 3</td>
                    <td>Linha 3</td>
                    <td>Linha 3</td>
                </tr>
            </tbody>
        </table>
    </section>
</main>

</template>