<template>
  <v-container>
    <v-card>
      <v-data-table :search="search" :headers="headers" :items="mDataArray">
        <!-- table top section -->
        <template v-slot:top>
          <v-toolbar flat color="white">
            <v-toolbar-title>Stock</v-toolbar-title>
            <v-divider class="mx-4" inset vertical></v-divider>
            <v-text-field
              v-model="search"
              append-icon="search"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
            <v-spacer></v-spacer>
            <v-btn
              @click="$router.push('/stock-create')"
              color="primary"
              dark
              class="mb-2"
            >
              <v-icon left>add</v-icon>
              <span>New Product</span>
            </v-btn>
          </v-toolbar>
        </template>

        <!-- table tr section -->
        <template v-slot:item="{ item }">
          <tr>
            <td>{{ item.id }}</td>
            <td>
              <v-img
                :src="item.image | imageUrl"
                aspect-ratio="1"
                max-width="50"
                max-height="50"
              ></v-img>
            </td>
            <td>{{ item.name }}</td>
            <td>{{ item.price | currency("฿") }}</td>
            <td>{{ item.stock | number("0,0") }} pcs.</td>
            <td>
              <v-icon class="mr-2" @click="editItem(item)">
                edit
              </v-icon>
              <span class="ma-1"></span>
              <v-icon @click="deleteItem(item)">
                delete
              </v-icon>
            </td>
          </tr>
        </template>
      </v-data-table>

      <v-dialog v-model="confirmDeleteDlg" max-width="290">
        <v-card>
          <v-card-title primary-title>
            Confirm Delete
          </v-card-title>

          <v-card-text class="body">
            Are you sure to delete this product? You cannot restore it after
            clicking confirm.
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn text @click="confirmDeleteDlg = false">
              Cancel
            </v-btn>

            <v-btn color="error" text @click="confirmDelete">
              Confirm
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-card>
  </v-container>
</template>

<script>
import api from "@/services/api";
// import StockModal from "@/components/dailog/StockModal";

export default {
  name: "Stock",
  data() {
    return {
      isSShowtockModal:false,
      search: "",
      selectedProductId: "",
      confirmDeleteDlg: false,
      mDataArray: [],
      headers: [
        {
          text: "Id",
          align: "left",
          sortable: false,
          value: "id"
        },
        { text: "Image", value: "image" },
        { text: "Name", value: "name" },
        { text: "Price", value: "price" },
        { text: "Stock", value: "stock" },
        { text: "Action", value: "action" }
      ]
    };
  },
  components: {
    // StockModal
  },
  
  async mounted() {
    this.loadProducts();
  },
  methods: {
    editItem(item) {
      this.$router.push(`/stock-edit/${item.id}`);
    },
    deleteItem(item) {
      this.selectedProductId = item.id;
      this.confirmDeleteDlg = true;
    },
    async confirmDelete() {
      await api.deleteProduct(this.selectedProductId);
      this.confirmDeleteDlg = false;
      this.loadProducts();
    },
    async loadProducts() {
      let result = await api.getProducts();
      this.mDataArray = result.data;
    }
  }
};
</script>

<style></style>
