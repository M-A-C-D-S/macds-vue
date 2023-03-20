<template>
    <div :class="{'cliente': !isPremium,'cliente-premium': isPremium}">
        <h4>Nome: {{cliente.nome}}</h4>
        <hr>
        <p>Número: {{cliente.numero}}</p>
        <p>Email: {{cliente.email}}</p>
        <p v-if="showAge === true">Idade: {{cliente.idade}}</p>
        <p v-else>O usuário escondeu a idade</p>
        <button @click="mudarCor($event)">Mudar cor</button>
        <button @click="emitirEventoDelete">Deletar</button>
        <h4>Id Especial: {{idEspecial}}</h4>
        <br>
        <hr>
        <br>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    data(){
        return {
           isPremium: false
        }
    },
    props: {
        cliente: Object,
        showAge: Boolean,
        showEmail: Boolean
    },
    methods: {
        mudarCor: function($event){
            console.log($event)
            this.isPremium = !this.isPremium //this serve para pegar variáveis num componente(isPremium é uma variável de data())
        },
        emitirEventoDelete: function(){
            this.$emit('Delete',{idDoCliente: this.cliente.id,curso: 'Node.js', emPromocao: true, component: this})//É um evento - Passa dados do filho para o pai
        },
        testar: function(){
            console.log('Testando passagem de método para pai')
            alert('Teste de passagem para Pai')
        }
    },
    computed: {
        idEspecial: function(){
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase()
        }
    }
}
</script>

<style scoped>
    .cliente {
        color:rgb(89, 0, 255)
    }

    .cliente-premium {
        color: brown;
        font-style: italic;
    }
</style>