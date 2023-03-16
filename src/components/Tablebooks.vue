<template>
    <div>
        <div id="burger-table">
            <Message
                :msg="msg"
                :corBackground="corBackgroudTablebooks"
                :corTexto="corTexoTablebooks"
                v-show="msg"
            
            />
            <div>
                <div id="burger-table-heading">
                    <div class="order-i">#:</div>
                    <div>Nome do Livro</div>
                    <div>Ano </div>
                    <div>Autor do Livro </div>
                    <div>Qnt de Paginas</div>
                    <div>Acões</div>
                </div>
            </div>

            <div id="burger-table-rows">
                <div class="burger-table-row" v-for="book in books" :key="book.id"> 
                    <div class="order-number">{{ book.id }}</div>
                    <div>{{ book.nomeLivro }}</div>
                    <div>{{ book.anoLivro }}</div>
                    <div>{{ book.autorLivro }}</div>
                    <div>{{ book.paginasLivro }}</div>
                    <div>
                        <button class="editar-btn">
                            Editar
                        </button>

                        <button class="delete-btn" @click="deleteBook(book.id)">
                            Deletar
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import api from '../api/api.js'
    import Message from './Message.vue'

    export default {
        name: "TableBooks",
        components: {
            Message
        },

        data() {
            return {
                books:null,
                msg: '',
                corBackgroudTablebooks:null,
                corTexoTablebooks: null
            }
        },

        methods: {
            async getbooks() {
                api.get("api/")
                .then((res) => {
                    this.books = res.data
                })
                .catch((error) => {
                    console.log(error)
                })
            },

            async deleteBook(id) {
                // ta assim pq so passei o numero do id na url no back end
                api.delete(`api/${id}`)
                .then((res) => {
                    console.log(res.data)
                    this.getbooks()
                })
                .catch(error => {
                    console.log(error)
                })

                // messagem e depois o tempo da mgs sair
                this.msg = `O livro foi excluido da Biblioteca`
                this.corBackgroudTablebooks = '#c9361c'
                this.corTexoTablebooks = '#edeef5'

                setTimeout (() => {
                    this.msg = ''
                    this.corBackgroudTablebooks = ''
                    this.corTexoTablebooks = ''
                }, 5000)



            }
        },

        mounted() {
            this.getbooks()

        }
    }
</script>

<style scoped>

#burger-table{
        max-width: 900px;
        margin: 0 auto;
    }

    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #burger-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;

    }

    #burger-table-heading div,
    .burger-table-row div {
        width: 16.6%;
    }

    .burger-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 16%;

    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
    }

    .editar-btn {
        background-color: #222;
        color: #7aae48;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 14px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
        margin-right: 7px;
        border-radius: 5px;
    }

    .editar-btn:hover {
        background-color: transparent;
        color: #222;
    }

    .delete-btn {
        background-color: #222;
        color: #f52525;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 14px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
        border-radius: 5px;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }

</style>