<template>
    <div>
        <Message 
            :msg="msg" 
            :corBackground="corBackgroundNoFormBooks" 
            :corTexto="corTextoNoFormBooks"
            v-show="msg" 
        />
        <div>
            <form action="" id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label for="nome-livro">Nome do Livro:</label>
                    <input type="text" id="nome-livro" name="nome-livro" 
                        v-model="nome_livro" placeholder="Digite Nome do Livro">
                </div>
    
                <div class="input-container">
                    <label for="ano-livro">Ano do Livro:</label>
                    <input type="text" id="ano-livro" name="ano-livro" 
                        v-model="ano_livro" placeholder="Digite Ano de Publicação">
                </div>
                
                <div class="input-container">
                    <label for="autor-livro">Autor do Livro:</label>
                    <input type="text" id="autor-livro" name="autor-livro" 
                        v-model="autor_livro" placeholder="Digite o Autor do Livro">
                </div>
    
                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Paginas do Livro:</label>
                    <input type="pags-livro" id="pags-livro" name="pags-livro" 
                        v-model="pags_livro" placeholder="Quantidade de Paginas do Livro">
                </div>
                <div class="input-button">
                    <input @click="createBook" type="submit" class="submit-btn" value="Adicionar Livro">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue'
import api from '@/api/api';

    export default {
        name: 'FormBoorks',
        components : {
            Message
        },
        
        data () {
            return {
                    nome_livro: null,
                    ano_livro:null,
                    autor_livro:null,
                    pags_livro:null,
                    msg:null,
                    corBackgroundNoFormBooks: null,
                    corTextoNoFormBooks: null
            }
        },

        methods : {
            async createBook (e) {
                e.preventDefault()


                // aqui ex o nomeLivro variavel do back end recebe o this.nome_livro
                // o que o usuario digitou no v-model no front
                const data = {
                    nomeLivro: this.nome_livro,
                    anoLivro: this.ano_livro,
                    autorLivro: this.autor_livro,
                    paginasLivro: this.pags_livro,
                    }

                if (data.nomeLivro && data.anoLivro && data.autorLivro && data.paginasLivro){
                    api.post('api/', data)
                        .then(response => {
                            console.log(response.data)
                        })
                        .catch(error => {
                            console.log(error.response.data)
                        })

                        //limpar os campos
                        this.nome_livro = ''
                        this.ano_livro = ''
                        this.autor_livro = ''
                        this.pags_livro = ''

                        // menssagem de sucesso
                        this.msg = `O livro ${this.nome_livro} foi Adicionado a Biblioteca`
                        this.corBackgroundNoFormBooks = '#41b05d'
                        this.corTextoNoFormBooks = '#1a20c9'
                        
                        setTimeout(() => {
                            this.msg = ""
                            this.corBackgroundNoFormBooks = ""
                            this.corTextoNoFormBooks = ""
                        }, 5000)

                    } else {
                        this.msg = 'Preencha todos os campos'
                        this.corBackgroundNoFormBooks = '#c9361c'
                        this.corTextoNoFormBooks = '#edeef5'

                    setTimeout(() => {
                        this.msg = ""
                        this.corBackgroundNoFormBooks = ''
                        this.corTextoNoFormBooks = ''
                    }, 5000)
                }
            }
        }
    }
</script>

<style scoped>
    #burger-form {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-button {
        flex-direction: column;
        margin-left: 60px;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #cb5729;
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }


    .submit-btn {
        background-color: #222;
        color: #cb5729;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
        border-radius: 5px;
        width: 185px;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }



</style>
