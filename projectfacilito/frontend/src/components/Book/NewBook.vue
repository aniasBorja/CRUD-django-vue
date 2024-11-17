<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col text-left">
                <h2>Nuevo Libro</h2>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <div class="card">
                    <div class="card-body">
                        <form @submit="onSubmit">
                            <div class="form-group row">
                                <label for="tittle" class="col-sm-2 col-form-label" >Titulo</label>
                                <div class="col-sm-6">
                                    <input type="text" placeholder="Titulo" name="title" class="form-control" v-model.trim="form.title">
                                </div>
                            </div>
                            <div class="form-group row">
                                <label for="description" class="col-sm-2 col-form-label">Descripción</label>
                                <div class="col-sm-6">
                                    <textarea name="description" class="form-control" placeholder="Descripción" rows="3" v-model.trim="form.description">
                                    </textarea>
                                </div>
                            </div>
                            <div class="rows">
                                <div class="col text-left">                                  
                                        <button type="submit" class="btn btn-primary ">Crear</button>
                                    <router-link :to="{ name: 'ListBook' }">
                                        <button type="button" class="btn btn-primary btn-dangerS">Cancelar</button>
                                    </router-link>
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
import axios from 'axios';
import swal from 'sweetalert'
export default{
    data() {
        return {
            form: {
                title: '',
                description: ''
            }
        }
    },

    methods:{
        onSubmit(evt){

            evt.preventDefault()

            const path = `http://localhost:8000/api/v1.0/books/`

           axios.post(path, this.form).then((response) =>{

            this.form.title = response.data.title
            this.form.description = response.data.description

            swal("Libro creado exitosamente", "","success")
            location.href='/books'
           })
           .catch((error)=>{
            swal("El Libro no creado ", "","error")
            console.log(error)
           })
        },

    },
    created(){
    }
    
}
</script>
<style lang="css" scoped>
</style>