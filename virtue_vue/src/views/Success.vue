<template>
    <div class="page-success">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Pedido bem sucedido!</h1>

                <p>Seu pedido foi efetuado com sucesso e está sendo processado</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Success',
    mounted() {
        document.title = 'Success | Vue shop'
    },
}
</script>