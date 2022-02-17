<template>
  <div class="shopping">
    <h1>{{msg}}</h1>
    <p>Quantidade : {{ productsCount }}</p>
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>Produto</th>
          <th>Quantidade</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{product.id}}</td>
          <td>{{product.name}}</td>
          <td class="center">
            <button @click="product.quant--">-</button>
            <input class="cell-center" min="0" type="number" v-model="product.quant">
            <button @click="product.quant++">+</button>
          </td>
          <td>{{total(product)}}</td>
        </tr>
      </tbody>
    </table>
    <p>Total: {{productTotal}}</p>
  </div>
</template>

<script>
export default {
  name: "Shopping",
  props: {
    msg: String
  },
  data() {
    return {
      products: [
        { id: 1, name: "Sapato", quant: 0, price: 189.98},
        { id: 2, name: "Bolsa", quant: 0, price: 120.98},
        { id: 3, name: "Camisa", quant: 0, price: 120.98},
        { id: 4, name: "Óculos", quant: 0, price: 50.98},
        { id: 5, name: "Shorts", quant: 0, price: 189.98},
      ]
    }
  },
  methods: {
    total(product){
      return (product.price * product.quant).toFixed(2)
    }
  },
  computed: {
    productsCount(){
      return this.products
      .map(product => product.quant)
      .reduce((pv,cv) => pv += cv)
    }, 
    productTotal(){
      return this.products
      .map(product => product.quant * product.price)
      .reduce((pv, cv) => pv += cv)
      .toFixed(2)
    }
  }
}
</script>

<style scoped>
.center {
  text-align:center
}
.cell-center {
  max-width: 30px;
}
h3 {
  margin: 40px 0 0
}
th,td{
  border-top: 1px solid lightgrey;
  padding: 5px 10px;
}
</style>