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
                                <v-icon v-if="item.Poster" :color="checkStart(item.imdbID) == undefined ? 'grey' : 'red' " @click="setStar(item)">star</v-icon>
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
                stars : [],
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
            },
            stars :{
                handler(){
                    this.$emit('push-stars',this.stars);
                },
                deep :true
            }

        },
        methods : {
            checkStart(imdbID){
                return this.stars.find(star => star.imdbID == imdbID);
            },
            setStar(item){
            
                let index = this.stars.find(star => star.imdbID == item.imdbID);
                if(index != undefined){
                    this.stars.map((star,index)=> {
                        if(star.imdbID == item.imdbID){
                            this.stars.splice(index,1);
                            return;
                        }
                    });
                    return;
                }else{
                    this.stars.push(item);
                    return;
                }
            }
        }

    }
</script>
<style scoped>
    .application--wrap{
        height: 200px !important;
    }
</style>