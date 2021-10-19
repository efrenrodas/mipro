<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <div class="card" style="width: 18rem">
         <div class="card-header">Crear nuevo</div>
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
           <form @submit.prevent="crear">
             <div class="row">
                 <div class="col-12 mb-2">
                     <div class="form-group">
                           <div class="mb-3">
                             <label for="exampleFormControlInput1" class="form-label">Titulo</label>
                             <input type="text" class="form-control" v-model="blog.titulo" placeholder="">
                            </div>
                            <div class="mb-3">
                            <label for="exampleFormControlTextarea1" class="form-label">Contenido</label>
                            <textarea class="form-control" v-model="blog.contenido" rows="3"></textarea>
                            </div>
                            <div class="col-12">
                                <button type="submit" class="btn btn-primary">Guardar</button>
                            </div>
                     </div>
                 </div>
             </div>
           </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
   name:"crear-blog",
   data(){
       return{
           blog:{
               titulo:"",
               contenido:""
           }
       }
   },
   methods:{
   async crear(){
      await     this.axios.post('/api/blog',this.blog)
           .then(response=>{
               this.$router.push({name:"mostrarBlogs"})
           })
           .catch(error=>{
               console.log(error())
           })
       }
   } 
};
</script>