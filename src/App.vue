<template>
    <div id="app">
        <Header/>
        <main class="container">
            <section class="drawer">
                <div class="drawer_container">
                    <!--<div><Pencil /></div>-->
                    <div>Eraser</div>
                    <div>Colors:
                        <div class="button-group button-row">
                            <button class="coloritem"
                                    v-for="colorItem in colors"
                                    :key="colorItem.display"
                                    :class="{ isActive: colorItem.color === chosenColor }"
                                    @click="selectColor"
                                    :data-color="colorItem.color"
                                    :style="{color: colorItem.color}"
                            >{{colorItem.display}}
                            </button>
                        </div>
                    </div>
                    <div class="gallery-item">
                        <button class="button-item">Gallery</button>
                    </div>
                </div>
            </section>
            <Canvas :currentColor="chosenColor" :availableColors="colors"/>
        </main>
    </div>
</template>

<script>

  import Header from './components/Header/Header.vue';
  import Canvas from './components/Canvas/Canvas.vue';
  import Pencil from './components/Buttons/Pencil.vue';

  export default {
    name: 'app',
    data() {
      return {
        chosenColor: '#000',
        isActive: false,
        colors: [
          { display: 'black', color: '#000' },
          { display: 'yellow', color: '#e8f904' },
          { display: 'blue', color: '#5e41f5' },
          { display: 'green', color: '#71b573' },
          { display: 'red', color: '#de4c0e' },
        ],
      }
    },
    methods: {
      selectColor(e) {
        this.isActive = !this.isActive;
        this.chosenColor = e.currentTarget.dataset.color
      }
    },
    components: {
      Header,
      Canvas,
      Pencil,
    }
  }
</script>

<style lang="scss">
    #app {
        height: 100%;
        background-color: #91ced0;
    }

    .container {
        display: flex;
        padding: 15px 20px 15px 15px;
    }

    .drawer {
        flex: 0 0 130px;
        &_container {
            padding-right: 15px;
        }
    }

    .gallery-item {
        .button-item {
            cursor: pointer;
            background-color: #1BF592;
            width: 100%;
            padding: 69px 0 15px;
            font-size: 1rem;
            color: white;

            &:hover {
                background-color: darken(#1BF592, 10%);
            }
        }
    }

    .button-group {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .coloritem {
        cursor: pointer;
        width: 60px;
        height: 50px;
        box-shadow: 1px 2px 1px 0 #9e9e9e;
        border: none;
        position: relative;

        &:first-child {
            border-top-left-radius: 2px;
            border-top-right-radius: 2px;
        }
        &:last-child {
            border-bottom-left-radius: 2px;
            border-bottom-right-radius: 2px;
        }

        &.isActive {
            &:before,
            &:after {
                content: '';
                background-color: green;
                width: 5px;
                height: 75%;
                position: absolute;
                top: 50%;
                transform: translateY(-50%);
            }
            &:before {
                left: -5px;
                border-top-left-radius: 2px;
                border-bottom-left-radius: 2px;
            }
            &:after {
                right: -5px;
                border-top-right-radius: 2px;
                border-bottom-right-radius: 2px;
            }
        }
    }
</style>
