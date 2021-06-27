<template>
  <v-dialog :value="visible" @input="closeModal" width="800px" v-bind:hide-overlay="false">
    <v-card class="mx-10  pa-5" outlined>
          <v-form @submit.prevent="submit">
            <v-text-field
              v-model="form.name"
              :counter="10"
              label="Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="form.price"
              suffix="THB"
              type="number"
              label="Price"
              required
            ></v-text-field>

            <v-text-field
              v-model="form.stock"
              suffix="PCS"
              type="number"
              label="Stock"
              required
            ></v-text-field>

            <input @change="onFileSelected" type="file" name="" id="" />
            <br />
            <v-img
              v-if="imageURL"
              :src="imageURL"
              height="200"
              width="200"
              class="mt-3"
            ></v-img>
            <br />
            <br />
            <v-row>
              <v-spacer></v-spacer>
              <v-btn class="mr-4" @click="cancel">
                Cancel
              </v-btn>

              <v-btn color="success" type="submit">
                Confirm
              </v-btn>
            </v-row>
          </v-form>
        </v-card>
  </v-dialog>
</template>

<script>

const initialForm = {
  name: "",
  price: "",
  stock: "",
      image: null
};

export default {
  props: {
    visible: {
      default: false,
      type: Boolean,
    },
    stock: null,
  },
  methods: {
    closeModal() {
      this.$emit("update:visible", false);
    },
    submit() {
      console.log('submit',this.$data.form);
      this.$emit('commit', this.$data.form);
      this.closeModal();
    },
    
  },
  mounted() {
   
  },
 
  watch: {
     visible() {
      console.log('stock',this.stock)
      if (this.stock) {
        this.$data.form = this.stock;
      } else {
        this.$data.form = JSON.parse(JSON.stringify(initialForm));
      }
    },
  },
  data() {
    return {
      form: {},
    };
  },
};
</script>

<style></style>
