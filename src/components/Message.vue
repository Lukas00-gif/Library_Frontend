<template>
    <div>
        <div class="message-container" 
            :style="{ backgroundColor: corBackground, color: corTexto }
        ">
                <p>{{ msg }}</p>
        </div>
    </div>
</template>

<script>
    export default  {
        name: "Message",

        props: {
            msg: { 
                type: String,
                required: true
            },

            corBackground: {
                type: String,
                required: false,
                default: '#CCE5FF'
            },
            corTexto: {
                type: String,
                required: false,
                default: '#004085'
            }
        }
    }
</script>

<style scoped>
    .message-container {
        border: 2px solid #B8DAFF;
        border-radius: 5px;
        padding: 10px;
        max-width: 340px;
        margin-left: 33%;
        margin-bottom: 2%;
        text-align: center;
    }
</style>