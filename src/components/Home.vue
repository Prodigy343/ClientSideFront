<template>
    <v-container class="pt-6">
        <v-row class="text-center">
            <v-col cols="4" offset="4">
                <v-text-field label="Search" dark v-model="searchWord"></v-text-field>
            </v-col>
        </v-row>

        <v-col v-if="find === undefined" class="text-center" cols="12">
            <div class="network-error white--text py-6">
                Some network connection error has ocurred. Please verify your API connection
            </div>
        </v-col>

        <v-row v-else class="text-center">
            <v-col cols="3">
                <div v-bind:style="imageContainer">
                    <v-img v-bind:style="logoImage1" class="mx-auto" src="@/assets/images/tvm-logo.png" max-width=180></v-img>
                </div>
                <div>
                    <v-progress-circular v-if="$apollo.queries.find && $apollo.queries.find.loading" indeterminate color="primary"></v-progress-circular>
                    <div v-else-if="find.tvmaze.length == 0" class="my-8 no-results">No results</div>
                    <v-card :show="true" transition="slide-y-transition" v-else v-for="item in find.tvmaze" :key="item.show.id" :href="item.show.url" target="_blank" rel="noreferrer noopener" class="mx-auto my-8 tvmaze-card" max-width="344">
                        <v-img v-if="item.show.image" class="white--text align-end" height="200px" position="center top" :src="item.show.image.medium">
                        </v-img>
                        <v-img v-else class="white--text align-end" height="200px" src="@/assets/images/placeholder.png">
                        </v-img>

                        <v-card-text>
                            <div class="card-title overline mb-4">{{item.show.name}}</div>
                            <p class="card-genre">Genre: {{ item.show.genres.length>0?item.show.genres[0]:'No genre' }}</p>
                            <div class="card-score">Score: {{item.score.toFixed(1)}}</div>
                        </v-card-text>
                    </v-card>
                </div>
            </v-col>

            <v-col cols="6">
                <div v-bind:style="imageContainer">
                    <v-img v-bind:style="logoImage2" class="mx-auto" src="@/assets/images/itunes-logo.svg" max-width=180></v-img>
                </div>
                <v-row>

                    <v-col cols="6">
                        <div class="category">Music</div>
                        <v-progress-circular v-if="$apollo.queries.find && $apollo.queries.find.loading" class="my-8" indeterminate color="primary"></v-progress-circular>
                        <div v-else-if="find.itunesMusic.length == 0" class="my-8 no-results">No results</div>
                        <v-card v-else v-for="item in find.itunesMusic" :key="item.id" class="mx-auto my-8 itunes-card" max-width="380">
                            <div class="d-flex flex-no-wrap justify-space-between">
                                <div class="content">
                                    <v-list-item-content class="text-left pl-3">
                                        <a :href="item.trackViewUrl" :title="item.trackName" target="_blank" class="overline mb-4">{{item.trackName}}</a>
                                        <v-list-item-subtitle>Artist: 
                                            <a :href="item.artistViewUrl" :title="item.artistName" target="_blank" rel="noopener noreferrer">{{item.artistName}}</a>
                                        </v-list-item-subtitle>
                                        <v-list-item-subtitle>Price: {{item.trackPrice===-1?'no price':item.trackPrice+item.currency}}</v-list-item-subtitle>
                                    </v-list-item-content>
                                </div>

                                <v-avatar class="my-3" size="100" tile>
                                    <a :href="item.trackViewUrl" :title="item.trackName" target="_blank" class="overline mb-4">
                                        <v-img :src="item.artworkUrl100"></v-img>
                                    </a>
                                </v-avatar>
                            </div>

                        </v-card>
                    </v-col>
                    <v-col cols="6">
                        <div class="category">Video</div>
                        <v-progress-circular v-if="$apollo.queries.find && $apollo.queries.find.loading" class="my-8" indeterminate color="primary"></v-progress-circular>
                        <div v-else-if="find.itunesMovie.length == 0" class="my-8 no-results">No results</div>
                        <v-card v-else v-for="item in find.itunesMovie" :key="item.id" class="mx-auto my-8 itunes-card" max-width="380">
                            <div class="d-flex flex-no-wrap justify-space-between">
                                <div class="content">
                                    <v-list-item-content class="text-left pl-3">
                                        <a :href="item.trackViewUrl" :title="item.trackName" target="_blank" class="overline mb-4">{{item.trackName}}</a>
                                        <v-list-item-subtitle>Artist: 
                                            <a :href="item.artistViewUrl" :title="item.artistName" target="_blank" rel="noopener noreferrer">{{item.artistName}}</a>
                                        </v-list-item-subtitle>
                                        <v-list-item-subtitle>Price: {{item.trackPrice}}{{item.currency}}</v-list-item-subtitle>
                                    </v-list-item-content>
                                </div>

                                <v-avatar class="my-3" size="100" tile>
                                    <a :href="item.trackViewUrl" :title="item.trackName" target="_blank" class="overline mb-4">
                                        <v-img :src="item.artworkUrl100"></v-img>
                                    </a>
                                </v-avatar>
                            </div>

                        </v-card>
                    </v-col>
                </v-row>
            </v-col>

            <v-col cols="3">
                <div v-bind:style="imageContainer">
                    <v-img v-bind:style="logoImage3" class="mx-auto logo-image" src="@/assets/images/crc-logo.png" max-height=60></v-img>
                </div>
                <div>
                    <v-progress-circular v-if="$apollo.queries.find && $apollo.queries.find.loading" class="my-8" indeterminate color="primary"></v-progress-circular>
                    <div v-else-if="find.crcind.length == 0" class="my-8 no-results">No results</div>
                    <v-card v-else v-for="item in find.crcind" :key="item.id" class="mx-auto my-8" max-width="344">
                        <v-list-item-content>
                            <div class="overline mb-4">{{item.name}}</div>
                            <v-list-item-subtitle>DOB: {{item.DOB}}</v-list-item-subtitle>
                            <v-list-item-subtitle>SSN: {{item.SSN}}</v-list-item-subtitle>
                        </v-list-item-content>
                    </v-card>

                </div>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    import gql from 'graphql-tag';
    export default {
        name: 'Home',
        methods:{},
        data(){
            return{
                searchWord: '',
                logoImage1:{
                    width: '100%',
                    maxWidth: '180px',
                    maxHeight: '140px',
                },
                logoImage2:{
                    width: '100%',
                    maxWidth: '100px',
                    transform: 'translateY(-20px)'
                },
                logoImage3:{
                    width: '100%',
                    maxWidth: '190px',
                    maxHeight: '120px',
                    transform: 'translateY(-20px)'
                },
                imageContainer:{
                    height: '120px',
                    paddingTop: '40px'
                }
            };
        },
        apollo:{
            find: {
                query: gql`query findByWord($searchWord: String!){
                    find(search: $searchWord){
                        itunesMusic{
                            artistId
                            artistName
                            collectionName
                            artistViewUrl
                            trackName
                            trackPrice
                            trackViewUrl
                            previewUrl
                            artworkUrl100
                            currency
                        }
                        itunesMovie{
                            artistId
                            artistName
                            collectionName
                            artistViewUrl
                            trackName
                            trackPrice
                            trackViewUrl
                            previewUrl
                            artworkUrl100
                            currency
                        }
                        tvmaze{
                            score
                            show{
                                id
                                url
                                name
                                genres
                                network{
                                    name
                                }
                                image{
                                    medium
                                }
                            }
                        }
                        crcind {
                            id
                            name
                            SSN
                            DOB
                        }
                    }
                }`,
                variables () {
                    return {
                        searchWord: this.searchWord,
                    }
                },
                // Additional options here
                fetchPolicy: 'cache-and-network',
            }
        },
        props: {
            msg: String
        }
    }
</script>