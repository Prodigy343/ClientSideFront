<template>
    <v-app>
        <v-main>
            <Home/>
        </v-main>
    </v-app>
</template>

<script>
import Home from './components/Home';

export default {
    name: 'App',

    components: {
        Home,
    },

    data: () => ({
        //
    }),
};
</script>

<style>
    a{
        text-decoration: none;
    }

    .v-main{
        background: #000046;  /* fallback for old browsers */
        background: -webkit-linear-gradient(to right, #1CB5E0, #000046);  /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(to right, #1CB5E0, #000046); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    }

    .itunes-card .v-avatar{
        justify-content: flex-end;
    }

    .itunes-card .overline{
        line-height: .9rem;
    }

    .tvmaze-card .card-title{
        color: black;
    }

    .tvmaze-card .card-genre{
        color: #F44336;
    }

    .tvmaze-card .card-score{
        color: #03A9F4;
    }

    .category{
        font-size: 22px;
        color: #FFFFFF;
        line-height: 1rem
    }

    .no-results{
        color: #A4A4A4;
        font-size: 16px;
    }

    body *{
        font-family: "Roboto", sans-serif;
        
    }

    @media only screen and (min-width: 500px) {
        .itunes-card .flex-no-wrap{
            width: 100%;
            min-width: 100%;
            flex-direction: column-reverse;
        }

        .itunes-card .v-avatar{
            min-width: 100%!important;
            margin: 0 auto;
            justify-content: center;
        }
        
        .itunes-card .v-list-item__subtitle{
            max-width: 100%;
        }

        .no-results{
            color: #A4A4A4;
            font-size: 20px;
        }

        .category{
            font-size: 26px;
        }
    }

    @media only screen and (min-width: 1264px) {
        .itunes-card .flex-no-wrap{
            width: 100%;
            min-width: 100%;
            flex-direction: initial;
        }

        .itunes-card .v-avatar{
            justify-content: flex-end;
            min-width: 100px!important;
            margin-right: 12px;
        }
        
        .itunes-card .v-list-item__subtitle{
            max-width: 130px;
        }

        .no-results{
            color: #A4A4A4;
            font-size: 22px;
        }

        .category{
            font-size: 28px;
        }
    }
</style>
