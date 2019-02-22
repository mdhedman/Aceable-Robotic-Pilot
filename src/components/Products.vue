<template>
  <div class="products">
    <b-container>
    <h2>View Robot Pilot Licensing Courses</h2>
    <div
      v-for="(product, index) in products"
      v-bind:key="product.id"
      v-bind="product"
      v-bind:index="index">
        <b-card >
          <h3 slot="header" class="mb-0">{{product.title}}</h3>
          <b-card-text>
          <b-container fluid >
            <b-row>
              <b-col cols="6">
                {{ product.description }}
              </b-col>
              <b-col cols="6">
                <b-container fluid>
                  <b-row>
                    <b-col cols="auto">
                      <h5>Price: ${{ formatPrice(product.price)}}</h5>
                    </b-col>
                    <b-col cols="auto">
                      <h5>Location: {{ product.state }}</h5>
                    </b-col>
                  </b-row>
                </b-container>
              </b-col>
            </b-row>
          </b-container>
          </b-card-text>
          <b-button href="#" variant="outline-primary" v-b-modal.nopurchase>Purchase</b-button>
        </b-card>
    </div>
    <b-modal id="nopurchase" title="Purchase Options">
    <p class="my-4">We're Sorry, Purchasing isn't available at this time.</p>
  </b-modal>
    <hr/>
    </b-container>
    </div>
</template>

<script>
export default {
  name: 'Products',
  data: function () {
    return {
      products: []
    }
  },
  mounted () {
    this.axios.get('https://mkt-endpoint.now.sh/products/').then(response => { this.products = sortedProducts(response.data) })
  },
  methods: {
    formatPrice (value) { return (value).toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',') }
  }
}
function sortedProducts (data) {
  return data.sort((t1, t2) => t1.price < t2.price ? -1 : 1)
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
