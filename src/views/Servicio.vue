<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';
import { METHODS } from 'http';


interface Productosdf {
    category: string;
    description: String;
    id: number;
    image: String;
    price: number;
    rating: {
        rate: number;
        count: number;
    };
    title: string;

};





const products = ref < Array < any >> ([]);

axios.get('https://fakestoreapi.com/products', {
    headers: {
        Autorization: '12366554',
        'KeyAuth': 'test1234'
    }
})
    .then(response => {
        console.log(response)
        products.value = response.data;
    })
    .catch(error => {
        console.log(error);
        alert('Error al consumir el servicio de productos');
    })
    .finally(() => {
        console.log('Se finalizó la consulta del servicio');
    })

function eliminar (id: number){
    axios.delete('https://fakestoreapi.com/products/'+ id)

    .then (response => {
        console.log(response);
        alert('Se ha eliminado el producto fictisio');
    })

    .catch(error => {
        console.log(error);
        alert('Error al tratar de eliminar un producto');
    });
    
}




 
</script>
<template>
    <div v-for="item of products">
        <img :src="item.image" alt="Producto">
        <button @click="eliminar (item.id)">Eliminar</button>
    </div>
</template>