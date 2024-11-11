<template lang="html">
    <div class="container">
        <div class="row" >
            <div class="col-md-12 text-left">
                <h2>Listado de Libros </h2>
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
                            <tr v-for="book in books" :key="book.id">
                            <td>{{ book.title }}</td>
                            <td>{{ book.description }}</td>
                            <td>
                                <button class="btn btn-primary btn-sm" @click="editItem(book)">Editar</button>
                                <button class="btn btn-primary btn-danger btn-sm" @click="editItem(book)">Eliminar</button>
                                

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

export default{
    data (){
        return {
            fields: [
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