<template>
  <div id="app">
    <h3>Cadastro:</h3>
    <small v-show="erro">O nome é inválido</small><br>
    <input type="text" placeholder="Nome" v-model="nomeField"><br>
    <input type="email" placeholder="Email" v-model="emailField"><br>
    <input type="number" placeholder="Idade" v-model="idadeField"><br>
    <button @click="cadastrarCliente">Cadastrar</button>
    <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
      <h4>{{index+1}}</h4>
      <Cliente :cliente="cliente" @Delete="deletarUsuario($event)"/>
    </div>
    
  </div>
</template>

<script>
import _ from 'lodash'
import Cliente from './components/Cliente.vue'
export default {
  name: 'App',
  data(){
    return {
      erro: false,
      nomeField: '',
      emailField: '',
      idadeField: 0,
    clientes: [
        {
          id: 1,
          nome: "Marcos Kaio",
          email: "mkaio@hotmail.com",
          idade: 17,
          showAge: true,
          showEmail: true,
          numero: 44
        },
        {
          id: 2,
          nome: "Lucas Jones",
          email: "lucas.jones222@hotmail.com",
          idade: 19,
          numero: 42
        },
        {
          id: 3,
          nome: "Luana Souza",
          email: "lsousz@hotmail.com",
          idade: 22,
          showAge: true,
          showEmail: true,
          numero: 39
        },
        {
          id: 4,
          nome: "Renan Piolinvk",
          email: "renan.p@live.com",
          idade: 14,
          showAge: true,
          showEmail: true,
          numero: 40
        },
      ]
    }
  },
  components: {
    Cliente
  },
  methods: {
    cadastrarCliente: function(){
      if(this.nomeField == "" || this.nomeField == "" || this.nomeField.lenght < 4){
        this.erro = true
      } else {
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now})
        this.nomeField = ""
        this.emailField = ""
        this.idadeField = 0
        this.erro = false
      }
    },
    deletarUsuario: function($event){
        console.log('A')
        console.log($event)
       var id = $event.idDoCliente
       var Deletar = this.clientes.filter(cliente => cliente.id != id)
       this.clientes = Deletar
      }
    },
    computed: {
      orderClientes: function(){
        return _.orderBy(this.clientes,['nome'],['asc'])
      }
    }
}
</script>

<style>
</style>
