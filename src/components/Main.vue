<template>
    <div>
        <div>
            <v-text-field append-icon="search" name="name" label="keywords" type="text" v-model="keywords"></v-text-field>
        </div>
        <v-alert v-if="messageError != null" style="color:red" :value="true" type="error">{{messageError}}</v-alert>
        <v-progress-circular
            v-if="loading"
            :size="50"
            color="primary"
            indeterminate
            ></v-progress-circular>
            <div v-else>
                    <v-layout row>
                    <v-flex xs12>
                        <v-card>
                        <v-list style="height:300px;overflow:auto">
                            <v-list-tile
                            v-for="(item,index) in items"
                            :key="index"
                            avatar
                            >
                            <v-list-tile-action>
                                <v-icon v-if="item.Poster" color="grey">star</v-icon>
                            </v-list-tile-action>
                
                            <v-list-tile-content>
                                <v-list-tile-title v-text="item.Title"></v-list-tile-title>
                            </v-list-tile-content>
                
                            <v-list-tile-avatar>
                                <img :src="item.Poster">
                            </v-list-tile-avatar>
                            </v-list-tile>
                        </v-list>
                        </v-card>
                    </v-flex>
                    </v-layout>
        </div>
    </div>  
</template>
<script>
    export default{
        data(){
            return {
                items : [],
                loading : true,
                keywords : '',
                loading : false,
                messageError : null
            }
        },
        watch : {
            keywords (){
                        var t = 500;
                    clearTimeout(window.popTimeout);
                        window.popTimeout = setTimeout( () => {
                        this.messageError = null;
                        this.loading = true;
                        axios.get('http://www.omdbapi.com/?i=tt3896198&apikey=3ae09044&s='+this.keywords)
                        .then(response=>{
                            if(response.data.Error){
                                this.messageError = response.data.Error;
                            }
                            this.items = response.data.Search;
                            this.loading = false;
                        });
                        },t);
            }                
        }
    }
</script>
<style scoped>
    .application--wrap{
        height: 200px !important;
    }
</style>