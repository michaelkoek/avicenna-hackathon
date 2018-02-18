<template>
    <div id="app">
        <Header/>
        <main class="container">
            <section class="drawer">
                <div>Pencil</div>
                <div>Eraser</div>
                <div>Colors:
                    <div class="button-group button-row">
                        <div class="button-item" v-for="colorItem in colors" :key="colorItem.display">
                            <button class="coloritem"
                                    @click="selectColor"
                                    :data-color="colorItem.color"
                            >{{colorItem.display}}</button>
                        </div>
                    </div>
                </div>
                <div>Gallery</div>
            </section>
            <Canvas :currentColor="chosenColor" :availableColors="colors"/>
        </main>
    </div>
</template>

<script>

  import Header from './components/Header/Header.vue';
  import Canvas from './components/Canvas/Canvas.vue';

  export default {
    name: 'app',
    data() {
      return {
        chosenColor: '#000',
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
        this.chosenColor = e.currentTarget.dataset.color
      }
    },
    components: {
      Header,
      Canvas
    }
  }
</script>

<style lang="scss">
    #app {
        height: 100vh;
        background-color: #91ced0;
    }

    .container {
        display: flex;
        padding: 20px;
    }

    .drawer {
        flex: 0 0 175px;
        background-color: purple;
    }
    .button-group {
        background-color: #EBEDF5;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>
