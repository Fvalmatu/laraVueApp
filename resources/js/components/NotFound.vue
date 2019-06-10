<style>
.imgnotfound {
    width: 600px;
    height: 100%;
}
</style>

<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-10 mt-4">
                <h3>No se encontro lo que anda buscando!</h3>
                <img v-bind:src="image" alt="" class="imgnotfound">
                
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                image: './img/notfound.jpg'
            }
        },

        mounted() {
            console.log('Component mounted.')
        }
    }
</script>