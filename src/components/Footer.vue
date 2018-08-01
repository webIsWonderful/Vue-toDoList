<template>
    <footer role="contentinfo">
        <p>{{ info }}</p>
        <span>&copy; {{ companyName }}</span>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
    data() {
        return{
            info: 'Ce footer doit rester en bas de la page.',
            companyName: 'Gremlins'
        }        
    }   
}
</script>

<style lang="scss" scoped>

footer {  
    display: grid;
    grid-template-columns: 1fr 100px;
    grid-column: 1/9;
    grid-row: 4;
    grid-gap: 10px;
    align-self: end;

    padding: 20px;
    background-color: #222222;

    font-weight: 400; 
    color: #ffffff;  
}

</style>
