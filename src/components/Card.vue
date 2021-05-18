<template>
    <div @click="flip()"  :class="{'flip-card': true, 'flipped': isFlipped, 'found': isCardFound}">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                X {{ id }}
            </div>
            <div class="flip-card-back" v-bind:style="{ backgroundImage: 'url(../assets/pexeso/1.jpg)' }">
                {{ id }}
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'Card',
        props: {
            id: Number,
            position: Number
        },

        methods: {
            flip() {
                this.$store.dispatch('cardFlip', this.position);
            }
        },

        computed: {
            isFlipped() {
                return this.$store.getters.isCardFlipped(this.position);
            },

            isCardFound() {
                return this.$store.getters.isCardFound(this.position);
            },

            canTurn() {
                return this.$store.getters.canTurn;
            }
        }
    }

</script>

<style lang="scss" scoped>
    .flip-card {
        background-color: transparent;
        border-radius: 4px;
        height: 100%;
        width: 100%;
        perspective: 1000px;
        cursor: pointer;

        &.found {
            visibility: hidden;
        }

        &-inner {
            position: relative;
            border-radius: 4px;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.8s;
            transform-style: preserve-3d;
        }

        &.flipped .flip-card-inner {
            transform: rotateY(180deg);
        }

        &-front, &-back {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            -webkit-backface-visibility: hidden; /* Safari */
            backface-visibility: hidden;
        }

        &-front {
            background-color: rgb(228, 228, 228);
            color: black;
        }

        &-back {
            background-color: dodgerblue;
            color: white;
            transform: rotateY(180deg);
        }
    }
</style>
