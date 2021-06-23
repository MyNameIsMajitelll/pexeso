<template>
    <div @click="flip()"  :class="{'flip-card': true, 'flipped': isFlipped, 'found': isCardFound}">
        <div class="flip-card-inner">
            <div class="flip-card-front" :style="{ backgroundImage: 'url(' + require('@/assets/cat-close-transparent.png') + ')' }">
                
            </div>
            <div 
                class="flip-card-back" 
                :style="{ backgroundImage: 'url(' + require('@/assets/pexeso/' + id + '.jpg') + ')' }">
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
            },
        
            imageUrl() {
                return `@/assets/pexeso/${this.id}.jpg`
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
            border-radius: 4px;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden; /* Safari */
            backface-visibility: hidden;
        }

        &-front {
            background-color: #f9e2ae;
            background-size: 50%;
            background-repeat: no-repeat;
            background-position: center center;
        }

        &-back {
            transform: rotateY(180deg);
            background-size: cover;
            background-repeat: no-repeat;
            background-position: center center;

        }
    }
</style>
