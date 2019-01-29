<template>
    <div id="app">
        <div class="title">
            Ты сегодня покормил кота?
        </div>
        <div class="card-list">
            <card-item
                v-for="item in goods"
                :key="item.id"
                :item="item">
            </card-item>
        </div>
    </div>
</template>

<script>
    //компонент для отображения карточки товара
    import CardItem from './components/CardItem.vue'

    import goods from './app.const'

    export default {
        name: 'app',
        data: function () {
            return { goods }
        },
        components: {
            CardItem
        }
    }
</script>

<style>
    @import "assets/css/style.css";
</style>
