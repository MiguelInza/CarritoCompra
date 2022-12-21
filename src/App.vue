<template>
  <div>
    <AppHeader :count="numberOfItems" />

    <!-- Crear el carrito -->
    <button @click="fetchApi">Obten Carrito</button>
    <form action="" @submit.prevent="validateForm()">
      <table>
        <thead>
          <tr>
            <th>index</th>
            <th>name</th>
            <th>photo</th>
            <th>price</th>
            <th>quantity</th>
            <th>total</th>
          </tr>
        </thead>
        <!--    {
            "uuid":"3",
            "name":"Vectorify",
            "description":"User Experience Design",
            "content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
            "image":"https://github.com/ironhack-jc/mid-term-api/blob/main/3.jpg?raw=true",
            "purshased_at":"June 10, 2021",
          "price": 5.50,
          "quantity":1,
          "active": true
        }, 
   -->
        <tbody>
          <tr v-for="(item, index) of items" :key="index">
            <td>{{ index }}</td>
            <td>{{ item.name }}</td>
            <td><img :src="item.image" :alt="item.name" width="70" /></td>
            <td>{{ item.price }}€</td>
            <td>
              <button @click="decrementQuantity(item)" type="button">-</button>

              <input
                type="number"
                v-model.number="item.quantity"
                placeholder="0"
              />

              <button @click="++item.quantity" type="button">+</button>
            </td>
            <td>{{ priceLine(item) }}€</td>
          </tr>
        </tbody>

        <tfoot>
          <tr>
            <th colspan="6">Total: {{ total }}€</th>
          </tr>
        </tfoot>
      </table>
      <button type="submit">Confirmar compra</button>
    </form>

    <!-- <app-footer /> -->
    <AppFooter :isMobile="!isDesktop" :submenu="menu" />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppFooter from "./components/AppFooter.vue";

const API_URL =
  "https://raw.githubusercontent.com/ironhack-jc/mid-term-api/main/cart";

export default {
  components: {
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      items: [],
      isDesktop: true,
      menu: ["Productos", "Servicios", "Contacta"],
    };
  },
  computed: {
    numberOfItems() {
      let sum = 0;

      for (const item of this.items) {
        sum += item.quantity;
      }

      return sum;
    },
    total() {
      /**
      let sum = 0;

      for (let index = 0; index < this.items.length; ++index) {
        const item = this.items[index];
        sum += item.price * item.quantity;
      }

      for (let index = 0; index < this.items.length; ++index) {        
        sum += this.items[index].price * this.items[index].quantity;
      }

      this.items.forEach(function (item) {
        sum += item.price * item.quantity;
      });

      this.items.forEach((item) => {
        sum += item.price * item.quantity;
      });

      for (const item of this.items) {
        sum += item.price * item.quantity;
      }

      return this.items.reduce(function (accumulator, item) {
        return accumulator + item.price * item.quantity;
      }, 0);

      return sum;
       */

      /** 
      return this.items.reduce(
        (accumulator, item) => accumulator + item.price * item.quantity,
        0
      );
      */

      return this.items.reduce(function (accumulator, item) {
        return accumulator + item.price * item.quantity;
      }, 0);
    },
  },
  methods: {
    async fetchApi() {
      const response = await fetch(API_URL);
      this.items = await response.json();
    },
    priceLine(item) {
      return item.price * item.quantity;
    },
    validateForm() {
      alert(`Hola`);
    },
    /**
     * Decrement the quantity by one but with a min of 0
     */
    decrementQuantity(item) {
      if (item.quantity > 0) {
        --item.quantity;
      }
    },
  },
  mounted() {
    this.fetchApi();
  },
};
</script>

<style scoped>
table {
  width: 100%;
}
table tfoot tr th {
  text-align: right;
}
</style>
