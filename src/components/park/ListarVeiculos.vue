<template>
   <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Placa
          </th>
          <th class="text-left">
            Hora/Entrada
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="veiculo in veiculos"
          :key="veiculo.placa"
        >
          <td>{{ veiculo.placa }}</td>
          <td>{{ veiculo.hora }}</td>
          <td><v-icon @click="sair(veiculo)">mdi-logout</v-icon></td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
export default {
    props: ['veiculos'],
    methods: {
      sair(veiculo) {
        this.$emit('sair', veiculo)
        this.$router.push()

      }
    }
}
</script>

<style>

</style>