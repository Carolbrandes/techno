<template>
    <section class="filters">
      <div>
        <h4>Categorias</h4>
         <div class="form-check">
          <input checked v-model="categorySelected" class="mr-2" type="checkbox" name="category" value="todos" id="todos" @change="handleCategorySelected">
          <label for="todos">Todos</label>
        </div>

        <div class="form-check"  v-for="(category, index) in this.$store.getters.productCategory" :key="index">
          <input v-model="categorySelected" class="mr-2" type="checkbox" name="category" :id="category" :value="category" @change="handleCategorySelected">
          <label :for="category">{{category}}</label>
        </div>
      </div>
    </section>
</template>

<script>
export default {
  created(){
    this.$store.dispatch("fetchProducts");
  },

  methods: {
    handleCategorySelected({target}){
      if(target.value === "todos"){
        console.log(this.$store.state.categorySelected)
        this.$store.commit("SET_CATEGORY",this.$store.state.categorySelected.filter(c => c === "todos"))
      }else{
        this.$store.commit("SET_CATEGORY",this.$store.state.categorySelected.filter(c => c !== "todos"))
      }
    }
  },

  computed: {
    categorySelected: {
      get(){
        return this.$store.state.categorySelected
      },
      set(value){
        this.$store.commit("SET_CATEGORY", value)
      }
    }
  }
}
</script>

<style scoped>
.filters{
  padding-top: 3rem;
}

h4{
  border-bottom: 1px solid #000;
  padding-bottom: 0.2rem;
  padding-left: 0.2rem;
  font-weight: bold;
}

.form-check{
  padding-top: 1rem;
  padding-left: 0.2rem;
}

@media screen and (min-width:1200px){
    .filters{
      width: 20vw;
      min-width: 200px;
      min-height: 100vh;
      border-right: 1px solid #000;
    }
}
</style>
