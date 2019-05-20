<template>
    <div class="hello">
        <h1>Consult Servers</h1>
        <input type="text" v-model="input.domain" placeholder="Domain Name" />
        <button v-on:click="sendData()">Consult</button>
        <br />
        <br />
        <textarea>{{ response }}</textarea>
         <br />
        <br />
        <h1>Consult Domains</h1>
        <button v-on:click="getDomains()">Get Data</button>
        <br />
        <br />
        <textarea>{{ response_Domain }}</textarea>
    </div>
  
        
</template>

<script>
    import axios from "axios";

    export default {
        name: 'HelloWorld',
        data () {
            return {
               response_Domain: "",
                input: {
                    domain: ""
                },
                response: ""
            }
        },
        methods: {
            sendData() {
              console.log('http://localhost:3333/server/'+this.input.domain )
                axios({ method: "GET", "url": 'http://localhost:3333/server/{'+this.input.domain +'}'}).then(result => {
                    this.response = result.data;
                }, error => {
                    console.error(error);
                });
            },

            getDomains() {
               axios({ method: "GET", "url": 'http://localhost:3333/servers'}).then(result => {
                    this.response_Domain = result.data;
                }, error => {
                    console.error(error);
                });
            }
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
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    textarea {
        width: 600px;
        height: 200px;
    }
</style>