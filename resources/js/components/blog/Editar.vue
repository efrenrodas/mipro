<template>
    <div class="row">
        <div class="col-12">
            <div class="card">
                <div class="card-header"><h4>Editar Blog</h4></div>
                <div class="card-body">
                    <form @submit.prevent="actualizar">
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
</template>

<script>
export default {
    name:"editarBlogs",
    data(){
        return {
            blog:{
                titulo:"",
                contenido:"",
            }
        }
    },
    mounted(){
        this.mostrarBlog()
    },
    methods:{
        async mostrarBlog(){
            await this.axios.get(`/api/blog/${this.$route.params.id}`).then(response=>{
                const { titulo, contenido } = response.data
                this.blog.titulo = titulo
                this.blog.contenido = contenido
            }).catch(error=>{
                console.log(error)
            })
        },
        async actualizar(){
            await this.axios.put(`/api/blog/${this.$route.params.id}`,this.blog).then(response=>{
                this.$router.push({name:"mostrarBlogs"})
            }).catch(error=>{
                console.log(error)
            })
        }
    }
}
</script>