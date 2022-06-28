<!-- <template>
  <h3>Produtos</h3>
  <hr />
  <ProductsInfo :products="products" v-slot="{ product }">
    <li @click="getProduct(product.id)">{{ product.name }}</li>
  </ProductsInfo>
</template>

<script setup>
import { reactive } from "vue";
import ProductsInfo from "../components/ProductsInfo.vue";

function getProduct(id) {
  alert("Id do Produto: " + id);
}

const products = reactive([
  {
    id: 1,
    name: "Imac",
  },

  {
    id: 2,
    name: "Mouse",
  },

  {
    id: 3,
    name: "Teclado",
  },
]);
</script> -->