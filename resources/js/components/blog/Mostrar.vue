<template>
<div class="container">


    <div class="row">
        
        <div class="col-12 mb-2">
            <router-link :to='{name:"crearBlogs"}' class="btn btn-success"><i class="fas fa-plus-square"></i></router-link>
        </div>
        <div class="col-12">
            <div class="table-responsive">
                <table class="table table-bordered">
                    <thead class="bg-primary text-white">
                        <th>Id</th>
                        <th>Titulo</th>
                        <th>Contenido</th>
                        <th>Acciones</th>
                    </thead>
                    <tbody>
                        <tr v-for="blog in blogs" :key="blog.id">
                            <td>{{blog.id}}</td>
                            <td>{{blog.titulo}}</td>
                            <td>{{blog.contenido}}</td>
                            <td>
                                <router-link :to='{name:"editarBlogs",params:{id:blog.id}}' class="btn btn-info">Editar </router-link>
                               <a type="button" @click="borrarBlog(blog.id)" class="btn btn-danger"> Borrar </a>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
    </div>
</template>

<script>


export default({
    name:"blogs",
    data(){
        return{
            blogs:[]
        }
    },
    mounted(){
        this.mostrarBlogs()
    },
    methods:{
      async  mostrarBlogs()
        {
        await   this.axios.get('/api/blog')
           .then(response=>{
               this.blogs=response.data
           })
           .catch(error=>{
               tihs.blog=[]
           })
        },
        borrarBlog(id){
          if(confirm ("confirma eliminar el registro")) {
              this.axios.delete('/api/blog/${id}')
              .then(response=>{
               this.mostrarBlogs
           })
           .catch(error=>{
              console
           })
          }
        }
    }
})
</script>
