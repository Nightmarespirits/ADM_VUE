<template>
  <v-card flat>
    <v-card-title class="d-flex align-center pe-2">
      <v-icon icon="mdi-video-input-component"></v-icon> &nbsp;
      Registros de Proceso Lavado

      <v-spacer></v-spacer>

      <v-text-field
        v-model="search"
        density="compact"
        label="Buscar"
        prepend-inner-icon="mdi-magnify"
        variant="solo-filled"
        flat
        hide-details
        single-line
      ></v-text-field>
    </v-card-title>

    <v-divider></v-divider>

    <v-data-table
      :search="search"   
      :headers="headers"
      :items="items"
      :items-per-page="items.length"   
    >
      <template v-slot:item.stock="{ item }">
          <div class="text-end">
            <v-chip
              :color="item.stock ? 'green' : 'red'"
              :text="item.stock ? 'In stock' : 'Out of stock'"
              class="text-uppercase"
              size="small"
              label
            ></v-chip>
          </div>
      </template>
      <template v-slot:item.details="{item}">
        <div>
          <v-btn variant="plain" @click="openDialog(item)">
            ver
          </v-btn>
        </div>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      search: '',   // Modelo de búsqueda
      headers: [
          {
            align: 'start',
            key: 'name',
            sortable: false,
            title: 'Fecha',
          },
          { key: 'image', title: 'Hora' },
          { key: 'price', title: 'Local' },
          { key: 'details', title: 'Detalles' },
          { key: 'rating', title: 'Responsable' },
          { key: 'stock', title: 'Estado' },
          
      ],
      items: [
        {
          name: 'Nebula GTX 3080',
          image: '1.png',
          price: 699.99,
          details: {

          },
          rating: 5,
          stock: true,
        },
        {
          name: 'Galaxy RTX 3080',
          image: '2.png',
          price: 799.99,
          rating: 4,
          stock: false,
        },
        {
          name: 'Orion RX 6800 XT',
          image: '3.png',
          price: 649.99,
          rating: 3,
          stock: true,
        },
        {
          name: 'Vortex RTX 3090',
          image: '4.png',
          price: 1499.99,
          rating: 4,
          stock: true,
        },
        {
          name: 'Cosmos GTX 1660 Super',
          image: '5.png',
          price: 299.99,
          rating: 4,
          stock: false,
        },
      ],
    };
  },
  methods: {
    openDialog(item) {
      this.$emit('open-dialog', item); // Emitir evento para que el padre lo escuche
    }
  }
};
</script>
