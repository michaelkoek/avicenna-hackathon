<template>
    <div id="app">
        <Header />
        <main class="container">
            <section class="drawer">
                <div>Pencil</div>
                <div>Eraser</div>
                <div>Colors:
                <button @click="selectColor" data-color="#000">Black</button>
                <button @click="selectColor" data-color="#e8f904">Yellow</button>
                <button @click="selectColor" data-color="#5e41f5">Blue</button>
                <button @click="selectColor" data-color="#71b573">Green</button>
                <button @click="selectColor" data-color="#de4c0e">Red</button>
                </div>
                <div>Gallery</div>
            </section>
            <Canvas :currentColor="chosenColor" />
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
</style>
