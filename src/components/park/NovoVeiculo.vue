<template>
    <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="novoVeiculo.placa"
            :counter="8"
            label="Placa do veículo"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          md="4"
        >
          <v-menu
        ref="menu"
        v-model="menu2"
        :close-on-content-click="false"
        :nudge-right="40"
        :return-value.sync="time"
        transition="scale-transition"
        offset-y
        max-width="290px"
        min-width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="novoVeiculo.hora"
            label="Picker in menu"
            prepend-icon="mdi-clock-time-four-outline"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-time-picker
          v-if="menu2"
          v-model="novoVeiculo.hora"
          full-width
          @click:minute="$refs.menu.save(time)"
        ></v-time-picker>
      </v-menu>
        </v-col>

      </v-row>
      <v-row>
          <v-col>
              <v-btn @click="salvar">Salvar</v-btn>
          </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
import * as fb from '@/plugins/firebase'
 export default{
    data: () => ({
      valid: false,
      novoVeiculo: {
          hora: new Date().toLocaleTimeString()
      },
      menu2: false,
      modal2: false,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),

    methods: {
      async salvar() {
            this.$emit('salvar', this.novoVeiculo)
            await fb.tasksCollection.add({
              placa: this.novoVeiculo.placa,
              hora: this.novoVeiculo.hora,
        })

        }
    },

}
 
    
 

    
</script>

<style>

</style>