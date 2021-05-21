<template>
  <div class="wrapper">

    <div class="intro" v-if="gameState === 'intro'">
        <div>
            <Cat />
        </div>
        hhyhyhyh
        <i>Od Románka pro Klárku.</i>

    </div> 
    
    <div class="home" v-if="gameState === 'home'">
        <div>
            <Cat />
        </div>

        <h1>{{ msg }}</h1>

        <div class="btns">
            <button @click="setSize({x: 2, y: 3})">I.</button>
            <button @click="setSize({x: 3, y: 4})">II.</button>
            <button @click="setSize({x: 4, y: 4})">III.</button>
            <button @click="setSize({x: 4, y: 5})">IV.</button>
        </div>
        <i>Od Románka pro Klárku.</i>

    </div> 
    
    <div class="is-playing" v-if="gameState === 'is-playing'">
        <div>
            <h1>{{ msg }}</h1>

            <table>
                <tr v-for="(item, indexY) in boardSize.y" :key="indexY">
                    <td v-for="(item, indexX) in boardSize.x" :key="indexX">
                        <Card :id="cardsShuffled[boardSize.x * indexY + indexX]" :position="boardSize.x * indexY + indexX" />
                    </td>
                </tr>
            </table>

            
            <button @click="backToHome()" style="background: green;width: 100px;height: 50px;border: 5px solid red;border-radius: 50px;">naspat</button>

            <transition name="fade">
                <div class="detail" v-if="cardDetail">
                    <CardDetail></CardDetail>
                </div>
            </transition>
            
        </div>
        
    </div>

    <div class="game-over" v-if="gameState === 'game-over'">
        <div>
            <h1 style="color:red">Tadaaaaa</h1>
            <img src="../assets/cat-close.png" alt="" /> <br>

            <button @click="backToHome()" style="background: green;width: 100px;height: 50px;border: 5px solid red;border-radius: 50px;">zpatki</button>
            <button @click="shuffle()" style="background: green;width: 100px;height: 50px;border: 5px solid red;border-radius: 50px;">znovu</button>
            
        </div>
    
    </div> 
  </div>

</template>

<script>

import Card from './Card';
import CardDetail from './CardDetail';
import Cat from './Cat';

export default {
  name: 'Wrapper',
  components: {
      Card,
      CardDetail,
      Cat
  },
  props: {
    msg: String
  },

  computed: {
    cardsShuffled() { return this.$store.state.cardsShuffled },
    boardSize() { return this.$store.state.size },
    isGameOver() { return this.$store.getters.isGameOver;  },
    gameState() { return this.$store.state.state;  },
    cardDetail() { return this.$store.state.cardDetail;  },
  },

  beforeMount() {},

  methods: {
    shuffle() {
      this.$store.dispatch('shuffle');
      this.$store.dispatch('play');
    },

    setSize(size) {
      this.$store.dispatch('setSize', size);
      this.$store.dispatch('play');
    },
    backToHome() {
        this.$store.dispatch('home');
    }
  }
}
</script>

<style lang="scss" scoped>
    $width: 350px;

    .fade-enter-active, .fade-leave-active {
       transition: opacity 1s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
    
    .wrapper {
        height: 100%;
        h1 {
            margin-bottom: 28px;
        }
    }
    .is-playing {
        position: relative;
        display: flex;
        height: 100%;
        flex-direction: column;
        justify-content: center;

        table {
            height: 350px;
            width: $width;
            margin: 0 auto;
            margin-bottom: 32px;
            table-layout: fixed;

            td {
                text-align: center;
                padding: 4px;
            }
        }

        .detail {
            $widthDetail: $width - 20px;
            $heightDetail: 400px;

            position: absolute;
            height: $heightDetail;
            background: #f9e2ae;
            border: 10px solid #f9e2ae;
            width: $widthDetail;
            left: calc(50% - #{$widthDetail/2} - 10px);
            top: calc(50% - #{$heightDetail/2});
        }
    }

    .home {
        display: flex;
        height: 100%;
        flex-direction: column;
        justify-content: center;
        margin: 20px 0;

        .btns {
            margin-bottom: 32px;

            button {
                cursor: pointer;
                background: #FAD2A1;
                color: #682B16;
                font-weight: 600;
                width: 60px;
                height: 60px;
                text-align: center;
                padding: 6px 0;
                font-size: 16px;
                line-height: 1.428571429;
                border-radius: 4px;
                margin: 0 4px;
                border: none;
            }
        }
        
    }

    .game-over {
        display: flex;
        height: 100%;
        flex-direction: column;
        justify-content: center;

        img {
            margin-bottom: 32px;
        }
    }

</style>
