<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col">
                <h3>Estas seguro de eliminar</h3>
                <p>Titulo: {{this.element.title}}</p>
                <p>Description: {{ this.element.description }}</p>
            </div>

        </div>
        <div class="row">
        <div class="col">
            <b-button @click="deleteBook" variant="danger">Eliminar 

            </b-button>
        </div>

        </div>
    </div>
   
</template>
<script>
import axios from 'axios'
import xwal from 'sweetalert'

export default {
    data () {
        return{
            bookId: this.$route.params.bookId,
            element: {
                title: '',
                description:''
            }
        }
    },
    methods: {
        getBook(){
            const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`

           axios.get(path).then((response) =>{
            this.element.title = response.data.title
            this.element.description = response.data.description
           })
           .catch((error)=>{
            console.log(error)
           })
        },
        deleteBook(){
            const path = `http://localhost:8000/api/v1.0/books/${this.bookId}/`

            axios.delete(path).then((response) =>{
                swal("Se ha eliminado correctamente", "", "Listo")
                location.href='/books'
            })
            .catch((error) => {
                swal("No es posible Eliminar el libro", "", "error")
            })
            }
        
        },
    created(){
        this.getBook()
    }

}
</script>
<style lang="css" scoped>
</style>