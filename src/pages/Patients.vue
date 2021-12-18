<template>
  <q-page class="flex flex-center">
    <q-table
      title="Pacientes"
      :rows="rows"
      :columns="columns"
      row-key="id"
      class="q-my-lg"
    />
  </q-page>
</template>

<script>
import axios from 'axios';
import { defineComponent } from 'vue';

const maxItems = 50;

const columns = [
  { name: 'name', align: 'center', label: 'Nome', field: 'name', sortable: true },
  { name: 'gender', align: 'center', label: 'Gênero', field: 'gender', sortable: true },
  { name: 'address', align: 'center', label: 'Endereço', field: 'address' },
  { name: 'city', align: 'center', label: 'Cidade', field: 'city' },
  { name: 'state', align: 'center', label: 'Estado', field: 'state' },
  { name: 'country', align: 'center', label: 'País', field: 'country', sortable: true },
  { name: 'email', align: 'center', label: 'E-mail', field: 'email', sortable: true },
  { name: 'phone', align: 'center', label: 'Telefone', field: 'phone', sortable: true },
  //{ name: 'id', align: 'center', label: 'ID', field: 'id', sortable: true },
  { name: 'date', align: 'center', label: 'Data de Nasc', field: 'date', sortable: true }
];

const rows = [];

export default defineComponent({
  name: 'PagePatients',
  setup () {
    return {
      columns,
      rows
    }
  },
  mounted () {
    if (rows.length < maxItems) {
        for (let index = 0; index < maxItems; index++) {
          axios.get('https://randomuser.me/api/')
            .then((response) => {
              console.log(response.data.results[0]);
              let result = response.data.results[0];
              let gender = '';
              if (result.gender === 'male') {
                gender = 'Masculino';
              }
              else {
                gender = 'Feminino';
              }
              let name = result.name.first + ' ' + result.name.last;
              let address = result.location.street.name + ', ' + result.location.street.number;
              let city = result.location.city;
              let state = result.location.state;
              let country = result.location.country;
              let email = result.email;
              let phone = result.phone;
              //let id = result.id.value;
              let date = result.dob.date.split('T')[0];
              let newRow = {
                gender: gender,
                name: name,
                address: address,
                city: city,
                state: state,
                country: country,
                email: email,
                phone: phone,
                //id: id,
                date: date,
              }
              rows.push(newRow);
            });
        }
    }
  }
})
</script>