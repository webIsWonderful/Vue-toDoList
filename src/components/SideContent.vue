<template>
     <aside role="complementary">
        <h3>{{ label }} :</h3>
        <p>
            Le but de cet exercice est d'améliorer cette interface (page totale) de manière à ce qu'elle soit
            <span>accessible</span> et <span>responsive</span>.
            De plus, vous pouvez modifier le HTML et le CSS comme vous le souhaitez.
        </p>
        <p>
            La maquette vous est fournie seulement pour la To Do List. <span>Pour le reste, vous êtes libre</span> !
        </p>
        <p>
            Attention ! Les objets de la liste doivent être rangés, d'abord par <span>statut (non fini ou fini)</span>, 
            puis par <span>ordre alphabétique</span>.
        </p>
    </aside> 
</template>

<script>
export default {
    name: 'SideContent',
    data() {
        return{
            label: "énoncé"
        }
    }   
}
</script>

<style lang="scss" scoped>

aside{
    grid-column: 3/5;
    grid-row: 2/3;
    margin: 42px 0 0 0;

    p{
      margin: 10px 0;
      padding: 14px 17px;
      
      color: #3E5252;
      line-height: 1.3rem;

      background-color: #E0EDF4;
      border-left: 5px solid #3EB3F6;

      span{
          font-weight: 900;
          color: #000000;
      }
    }

    h3{
      text-transform: capitalize;
      font-size: 1.5rem;
      font-weight: 700;
    }
}

/* Media Queries */

@media (max-width : 1320px){
    aside{
        grid-column: 2/5;
    }
}

@media (max-width : 900px){
    aside{
        grid-column: 1/5;
        padding-left: 30px;
    }
}

@media (max-width : 760px){
    aside{
        grid-column: 1/9;
        grid-row: 3;

        margin-top: 0;
        padding:  0 30px;
        
    }
}

</style>
