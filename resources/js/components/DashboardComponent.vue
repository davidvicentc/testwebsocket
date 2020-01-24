a<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                hola
                <div v-for="item in items">
                    <h3>{{item.title}}</h3>
                    <p>{{item.description}}</p>
                </div>
                <div>
                    <input type="text" placeholder="title" v-model='itemToAdd.title'>
                    <input type="text" placeholder="description" v-model='itemToAdd.description'>
                    <button @click="addItem">Enviar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                items: [],
                itemToAdd: {}
            }
        },
        mounted() {
            window.Echo.channel('items')
                .listen('ItemDemo', (e) => {
                    console.log('e', e)
                    this.items = e.items
                })
        },
        methods: {
            addItem() {
                axios.post('/', {
                    title: this.itemToAdd.title,
                    description: this.itemToAdd.description,
                }).then((result) => {
                    console.log('sirve')
                    console.log('result', result)
                }).catch((e) => {
                    console.log(e)
                })
            }
        }
    }
</script>
