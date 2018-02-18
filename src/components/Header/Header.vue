<template>
    <header>
        <section class="header_container">
            <div class="header_logo">
                <img src="http://placehold.it/300x100" alt="logo printies">
            </div>
            <div class="header_actions">
                <div class="header_actions__person">
                    <button class="button-item">Person</button>
                </div>
                <div class="header_actions__handeling">
                    <button class="button-item">open</button>
                    <button class="button-item">save</button>
                    <button class="button-item">objects</button>
                </div>
            </div>
        </section>
    </header>
</template>

<style lang="scss">

    header {
        padding: 20px 20px 0;
    }

    .header_container {
        display: flex;
        align-items: center;
    }

    .header_logo {
        flex: 1 1 auto;
        position: relative;
        img {
            position: relative;
            top: 32px;
            left: 25%;
        }
    }
    .header_actions {
        flex: 1 1 auto;
        display: flex;
        &__person {
            flex: 1 0 auto;
        }

        .button-item {
            height: 45px;
            width: 45px;
            border: none;
            box-shadow: 1px 2px 1px 0 #9e9e9e;
            border-radius: 2px;
            cursor: pointer;
        }
    }


</style>
