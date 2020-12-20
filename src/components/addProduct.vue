<template>
    <div id="addProduct">
        
        <div class="title">
            <h2>Agregar Producto</h2>
        </div>

        <div class="buttons">
        <button v-on:click="procesarInicio">Inicio</button>
        </div>

        <div class="forms">
            <br>
            <h2>Codigo de barras</h2>
            <input v-model="product.bar_code" type="text" placeholder="">
            <h2>Nombre</h2>
            <input v-model="product.name" type="text" placeholder="">
            <h2>Precio</h2>
            <input v-model="product.price" type="text" placeholder="">
            <h2>Cantidad</h2>
            <input v-model="product.stock" type="text" placeholder="">
        </div>

        <div class="agregar">
            <button v-on:click="procesarAgregarProducto">Agregar</button>
        </div>

    </div>
    
    

</template>

<script>
import axios from 'axios';
    export default {
        name: "addProduct",
        data: function(){
            return{
                hay_datos: false,
                product: {
                    bar_code: "",
                    name: "",
                    price: "",
                    stock: ""

                }
            }
        },
        methods: {
            procesarInicio: function(){
                this.$router.push({name: "inicio"})
            },
            procesarAgregarProducto: function(){
                let self = this
                axios.post("https://inventario-api-g2m3-6.herokuapp.com/product/", {
                    bar_code: self.product.bar_code,
                    name: self.product.name,
                    price: self.product.price,
                    stock: self.product.stock
                })
                    .then((result)=>{
                        alert("El producto se ha agregado correctamente") 
                    })
                    .catch((error)=>{
                        self.hay_datos = false
                        alert("ERROR: " + error.response.status)
                    })

            }
        }
    }
</script>

<style>
.buttons{
    text-align: center;
    font-family: Arial, Helvetica, sans-serif;
    font-size: large;
  }
.agregar{
    text-align: center;
    font-family: Arial, Helvetica, sans-serif;
    font-size: large;
    }
.title{
    text-align: center;
    font-family: Arial, Helvetica, sans-serif;
    font-size: large;
  }
  .result{
    text-align: center;
    font-family: Arial, Helvetica, sans-serif;
    font-size: medium;
  }
.forms{
    text-align: center;
    font-family: Arial, Helvetica, sans-serif;
    font-size: small;
  }
</style>