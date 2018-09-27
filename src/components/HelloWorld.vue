<template>
    <div class="hello">
        <h1>Consuming mercadolibre API REST</h1>
        <input type="text" v-model="input" placeholder="Product name" />               
        <button v-on:click="Search()">Search</button>
        <br />
        <br />
        <div id="results">
            <ul v-for="response in responses">
                <li >
                    <h3> NAME:  {{ response.title }} </h3>  
                    <h3> PRICE: {{ response.price }} {{response.currency_id}} </h3>  
                    <img :src="response.thumbnail"> 
                    <h4> Access: {{response.permalink}}</h4>
                </li>
                <br>
                <br>
                <br>
            </ul>
        </div>
         


    </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: 'HelloWorld',
        data () {
            return {
               
                input: "",               
                responses:[]
                }
            
        },
        
        methods: {
           Search() { axios({ method: "GET", "url": "https://api.mercadolibre.com/sites/MLU/search?q="+this.input}).then(result => {
                    this.responses = result.data.results;
                }, error => {
                    console.error(error);
                });
        },
           
         }
    }
</script>

<style scoped>
    h1, h2 {
        font-weight: normal;
    }

    ul {
        list-style-type: none;
        padding: 0;
        text-align: left;
    }

    li {
        display: inline-block;
        margin: 0 10px;
        text-align: left;
    }

    a {
        color: #42b983;
    }

    textarea {
        width: 600px;
        height: 200px;
    }
    #results{
        margin:auto;
        width: 600px;
        height: 200px;
    }
</style>