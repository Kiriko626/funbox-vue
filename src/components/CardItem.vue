<template>
    <div class="card-item" :class="{'card-item--disabled':item.isDisabled}">
        <!--Карточка продукта-->
        <div class="card-product"
             @click="setActive"
             @mouseover="hoverCheck"
             @mouseout="item.isHover=false"
             :class="{'card-product--selected':item.isSelected}"
             tabindex="0"
        >
            <p class="card-product__note" v-if="!item.isHover">Сказочное заморское яство</p>
            <p class="card-product__note card-selected-text" v-if="item.isHover">Котэ не одобряет?</p>
            <h2 class="card-product__title">Нямушка <span>{{ item.title }}</span></h2>
            <ul class="card-product__bonus">
                <li><b>{{ item.amount }}</b> порций</li>
                <li>{{ item.present }}</li>
                <li v-if="item.extraPresent">{{ item.extraPresent }}</li>
            </ul>
            <img class="card-product__image" src="../assets/img/cat.png" :alt="'Нямушка '+item.title">

            <div class="card-product__weight">{{item.weight}}<br><span>кг</span></div>
        </div>

        <p class="card-item__note" v-if="!item.isDisabled && !item.isSelected">Чего сидишь? Порадуй котэ,
            <button class="card-item__btn-link" @click="setActive()" type="button">купи.</button>
        </p>
        <p class="card-item__note card-item__note--disabled" v-if="item.isSelected && !item.isDisabled">
            {{ item.selectedText }}</p>
        <p class="card-item__note card-item__note--disabled" v-if="item.isDisabled">Печалька, {{ item.title }}
            закончился.</p>
    </div>
</template>

<script>
    export default {
        name: 'CardItem',
        props: ['item'],
        methods: {
            //метод для смены состояния пачки
            //меняет статус при клике (только если не выключена)
            setActive: function () {
                this.item.isSelected = !this.item.isDisabled && !this.item.isSelected;
                this.item.isHover = false
            },

            //метод для изменения состояния наведения
            hoverCheck: function () {
                this.item.isHover = !!this.item.isSelected;
            }
        }
    }
</script>
<style lang="stylus">
    $main-color = #f2f2f2

    $linear-gradient-background($color)
        background linear-gradient(135deg, transparent 31px, $color 0);

    .card-product
        width 312px
        border-radius 10px
        padding-left 45px
        padding-right 45px
        padding-top 20px
        color #666666
        background-color $main-color
        $linear-gradient-background($main-color)
        min-height 472px
        margin-bottom 19px
        display block
        cursor pointer
        position relative
        outline none

        &::before
            content ''
            width 320px
            min-height 480px
            height calc(100% + 6px)
            z-index -1
            border-radius 10px
            position absolute
            top -4px
            left -4px
            $linear-gradient-background(#1698d9)

        &:hover::before
        &:focus::before
            $linear-gradient-background(#2ea8e6)

        &__note
            margin-top 0
            margin-bottom 19px
            font-size 16px
            line-height 18px

        &__title
            font-size 48px
            line-height 31px
            font-weight bold
            color #000000
            margin-top 0
            margin-bottom 12px

            span
                font-size 24px

        &__bonus
            list-style none
            padding 0
            margin-top 0
            margin-bottom 18px
            min-height 49px

        &__image
            display block
            margin-left -45px

        &__weight
            font-size 42px
            line-height 21px
            text-align center
            color #ffffff
            background-color #1698d9
            border-radius 50%
            width 81px
            height 81px
            padding 23px 5px
            position absolute
            bottom 11px
            right 11px

            span
                font-size 21px

        &--selected
            &::before
                $linear-gradient-background(#d91667)

            &:hover::before
            &:focus::before
                $linear-gradient-background(#e62e7a)

            .card-product__weight
                background-color #d91667

            &:hover
            &:focus
                .card-product__weight
                    background-color #e62e7a

    .card-item
        width 100%
        max-width 320px
        min-height 513px
        margin 0 auto 50px
        padding-top 4px
        padding-left 4px
        @media screen and (min-width: 720px)
            width 320px
            margin-left 0
            margin-right 0
        @media screen and (min-width: 1200px)
            margin-right 80px
            margin-bottom 0

            &:first-child
                margin-right 80px
                margin-bottom 0

            &:last-child
                margin-right 0

        &--disabled
            pointer-events none

            .card-product::before
            .card-product:focus::before
                $linear-gradient-background(#b3b3b3)

            .card-product__note
            .card-product__title
            .card-product__bonus
                color #b3b3b3

            .card-product__image
                opacity .5

            .card-product__weight
                background-color #b3b3b3

        &__note
            font-size 13px
            line-height 13px
            text-align center
            text-shadow -1px 2px 0 rgba(0, 0, 0, 1)
            color #ffffff
            margin 0

            &--disabled
                color #ffff66

        &__btn-link
            border none
            background-color transparent
            padding 0 0 1px
            color #1698d9
            font-weight bold
            border-bottom 1px dashed #1698d9
            text-shadow -1px 2px 0 rgba(0, 0, 0, 1)
            cursor pointer
</style>
