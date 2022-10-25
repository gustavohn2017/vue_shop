<template>
    <footer class="footer">
     <div class="has-text-centered">
        <p>Placeholder de rodapé, não sei que merda vou fazer aqui ainda.</p>
    </div>
</footer>
</template>
<style scoped>
    .footer{
        bottom: 0;

    }
    @media all and (max-width: 500px){
        .footer{
            bottom: 0;
            position:relative;
            padding-top: 15em;
            
        }
    
    }
</style>

<script>
export default {
  name: 'FooterSection',
};
</script>