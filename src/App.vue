<template>
<v-app class="corpo">
<img src="https://icones.pro/wp-content/uploads/2021/03/symbole-de-voiture-icone-png-vert.png" alt="" height="200" width="200">
    <nav class="titule"><b>Control Park</b></nav>

    <v-main class="tabela">
      <v-card
          :elevation="hover ? 24 : 6"
          class="mx-auto pa-6"
        >
      <v-container class="fnd">
        <novo-veiculo v-if="novoVeiculo" @salvar="adicionarVeiculo"/>
       <listar-veiculos v-else :veiculos="veiculos" @sair="sair" />
       
      </v-container>
      </v-card>
    <div class="botao">  
    <v-btn
      class="mx-2"
      fab
      dark
      color="green darken-1"
      v-if="!novoVeiculo"
      @click="novoVeiculo=true"
    >
      <v-icon dark>
        mdi-plus
      </v-icon>
    </v-btn>
    </div>
    
    </v-main>


  
</v-app> 
</template>

<script>
import ListarVeiculos from '@/components/park/ListarVeiculos'
import NovoVeiculo from '@/components/park/NovoVeiculo'
export default {
  components: { ListarVeiculos, NovoVeiculo },
  data() {
    return {
      novoVeiculo: false,
      veiculos:[
        
      ]
    }
  },
  methods: {
    sair(veiculo) {
      const v = this.veiculos.indexOf(veiculo)
      this.veiculos.splice(v, 1)
    },
    adicionarVeiculo(novoVeiculo) {
      this.veiculos.push(novoVeiculo)
      this.novoVeiculo = false
    }
  }
}
</script>
<style>
.card{
  background-color: grey;
  margin: auto;
  margin-top: 10px;
  border-radius: 5px;
  border-style: solid;
  border-width: 2px;
  border-color: grey;
  width: 400px;

}
.titule{
  margin: auto;
  margin-bottom: 5px;
  font-family: Trebuchet MS, sans-serif;
  font-size: 50px;
  color: green;
  
  
}
img{
  margin: auto;
}
.tabela{
  margin: auto;
}
.botao{
  margin-top: 20px;
 text-align: center;
}






</style>



