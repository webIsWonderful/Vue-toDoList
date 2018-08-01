<template>
    <header role="banner">
        <div class="wrapper">
            <h1>{{ msg }}</h1>
            <img v-bind:src="imgUrl" alt="oui-sncf logo" />            
        </div>
    </header>    
</template>

<script>
export default {
    name: 'MainHeader',
    data() {
        return{
            msg: 'Bienvenue à Ma Todo List !',
            imgUrl: "https://www.oui.sncf/sites/all/modules/custom_addons/vsct_feature_canvas/theme/dist/img/oui-sncf.svg"
        }        
    }   
}
</script>

<style lang="scss" scoped>

header{
    display: grid;
    grid-column: 1/9;
       
    font-family: 'Baloo', Helvetica, Arial, sans-serif;
    padding: 0 20px;
    
    box-shadow: 0 1px 18px rgba(0, 0, 0, 0.25); 

    .wrapper{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;

        & > * {
            flex-grow: 0;
        }
        h1{
            font-size: 2rem;
            color: #155532;
            justify-content: right;
            order: 1;
            padding-right: 100px;
        }

        img{
            display: block;
            width: 240px;
            padding-right: 100px;
        }
    }   
      
}

/* Media Queries */

@media (max-width : 780px){
    header{
        .wrapper{         
            h1{
                font-size: 1.6rem; 
                padding-right: 10px;           
            }

            img{
                padding-right: 10px;
                width: 150px;
            }
        }        
    }
}

@media (max-width : 540px){
    header{
        .wrapper{         
            h1{
                font-size: 1.2rem; 
                padding-right: 0;           
            }

            img{
                padding-right: 0;
                width: 120px;
            }
        }        
    }
}

</style>
