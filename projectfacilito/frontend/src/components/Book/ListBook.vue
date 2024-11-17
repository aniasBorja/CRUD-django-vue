<template lang="html">
    <div class="container">
        <div class="row" >
            <div class="col-md-12 text-left">
                <h2>Listado de Libros </h2>
                <router-link :to="{ name: 'NewBook'}" variant="Primary">
                    <button class="btn btn-success btn-sm">Nuevo Libro</button>
                </router-link>
                    <div class="col-md-12"> 
                        <!-- Tabla con Bootstrap 5 -->
                        <table class="table table-striped table-hover">
                        <thead>
                            <tr>
                            <th>Título</th>
                            <th>Autor</th>
                            <th>Acciones</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="book in books" >
                            <td>{{ book.title }}</td>
                            <td>{{ book.description }}</td>
                            <td>
                                <router-link :to="{ name: 'EditBook', params:{bookId: book.id}}">
                                <button class="btn btn-primary btn-sm">Editar</button> </router-link>
                                <router-link :to="{ name: 'DeleteBook', params:{bookId: book.id}}">
                                <button class="btn btn-primary btn-danger btn-sm"  >Eliminar</button></router-link>
                             </td>
                            </tr>
                        </tbody>
                        </table>
                    </div>
            </div>
        </div>
    </div>
</template>

<script >
import axios from 'axios';
import deleteBook from './DeleteBook.vue';
import EditBook  from './EditBook.vue';

export default{
    data (){
        return {
            books: [
                {key: 'title', label:'Título'},
                {key: 'description', label:'Descripción'},
                {key: 'action', label: 'Acción'}
            ], 
            books: []
        }
    },
    methods:{

        getBooks(){


            const path = 'http://localhost:8000/api/v1.0/books/'
            axios.get(path).then((response) => {
                this.books = response.data
            })
            .catch((error) =>{
                console.log(error)
            })
        }
    },

    created(){
        this.getBooks()
    }

}
</script>

<style lang="css" scoped>
</style>