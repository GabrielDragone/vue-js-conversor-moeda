<template>
    <div class="conversor">
        <h2>{{moedaA}} para {{moedaB}}</h2>
        <!-- o v-bind vincula o valor da moeda para aparecer no placeholder -->
        <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA"/>
        <input type="button" value="Converter" v-on:click="converter"/>
        <h2>{{moedaB_value}}</h2>
    </div>

</template>

<script>
    export default{
        name: "Conversor",
        props: ["moedaA", "moedaB"],
        data(){
            return{
                moedaA_value : "",
                moedaB_value : 0,
            };
        },
        methods: {
            converter(){
                
                let strDePara = this.moedaA + "_" + this.moedaB;

                console.log(strDePara);

                let url = 'https://free.currconv.com/api/v7/convert?q='+
                    strDePara
                    +'&compact=ultra&apiKey=4f7409236939317cd850';

                console.log(url);

                //Faz uma requisição pro endereço da API:
                fetch(url)
                    .then(res => {
                        return res.json();
                    })
                    .then(json => {
                        console.log(json);
                        let cotacao = json[strDePara].val;
                        console.log('Teste ' + cotacao);
                        this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(
                            2
                        );
                    });

            },
        }
    }
</script>

<!-- Escoped para o estilo ficar apenas nesse Component -->
<style escoped> 
    .conversor{
        margin: auto;
        max-width: 900px;
        padding: 20px;
        max-width: 300px;
        box-shadow: 0 4px 8px 0 rgb(0, 0, 0, 0.2);
    }
    .linha{
        margin-top: 40px;
        display: flex;
        justify-content: space-around;
    }
</style>