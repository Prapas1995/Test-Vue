<template>
  <v-container>
    <div class="wellcome">
      <v-row>
        <v-col lg="3" md="6" sm="12" cols="12">
          <StockCard
            title="TOTAL"
            subtitle="1,800"
            avatar_bg="#00a65a"
            avatar_ic="mdi-cart-outline"
          />
        </v-col>

        <v-col lg="3" md="6" sm="12" cols="12">
          <StockCard
            title="SOLD-OUT"
            avatar_ic="mdi-flask-empty-outline"
            avatar_bg="#f39c12"
            subtitle="12"
          />
        </v-col>

        <v-col lg="3" md="6" sm="12" cols="12">
          <StockCard
            title="RETURN"
            avatar_ic="mdi-keyboard-return"
            avatar_bg="#dd4b39"
            subtitle="2"
          />
        </v-col>

        <v-col lg="3" md="6" sm="12" cols="12">
          <StockCard
            title="DISCOUNT"
            avatar_ic="mdi-gift-outline"
            avatar_bg="#00c0ef"
            subtitle="101"
          />
        </v-col>
      </v-row>
      <h1> Welcome {{$store.getters["username"]}} to Vue.js</h1>
    </div>
  </v-container>
</template>

<script>
// import api from "@/services/api";
import StockCard from "@/components/cards/StockCard";

export default {
  name: "Stock",
  data() {
    return {
      search: "",
    };
  },
  components: {
    StockCard
  },
  
  async mounted() {
    this.loadProducts();
  },
  methods: {
    
  }
};
</script>