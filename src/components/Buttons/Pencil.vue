<template>

    <div id="pencil_wrapper" class="green">
        <div class="shaft"></div>
        <div class="point"></div>
        <div class="lead"></div>
    </div>
</template>

<style lang="scss">

    // @src: https://codepen.io/Irusik/pen/uwKGs

    #pencil_wrapper {
        position: absolute;
        top: 20px;
        left: 12px;
        width: 50px;
        margin-left: 100px;
        transform: rotate(-90deg);
    }

    .shaft {
        position: relative;
        top: 0;
        width: 21px;
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 10px;
        z-index: 1;


        &:before,
        &:after {
            position: absolute;
            content: '';
            width: 10px;
        }

        &:before {
            left: -12px;
            border-top-left-radius: 4px;
            border-bottom-right-radius: 10px;
        }

        &:after {
            left: 21px;
            border-top-right-radius: 2px;
            border-bottom-left-radius: 8px;
        }
    }

    .shaft,
    .shaft:before,
    .shaft:after {
        top: 0;
        height: 175px;
    }

    .point {
        position: relative;
        top: -2px;
        left: -12px;
        width: 0;
        height: 0;
        border-top: solid 40px rgba(202, 176, 147, 1);
        border-right: solid 22.5px rgba(202, 176, 147, 0);
        border-left: solid 22.5px rgba(202, 176, 147, 0);
    }

    .point:before {
        position: absolute;
        content: "";
        top: -50px;
        left: -18px;
        width: 35px;
        height: 10px;
        background: rgba(197, 173, 145, 1);
    }

    .point:after {
        position: absolute;
        content: "";
        top: -49px;
        left: -15px;
        width: 30px;
        height: 40px;
        background: linear-gradient(to right, rgba(208, 181, 159, 0.65) 0%, rgba(253, 231, 213, 1) 40%, rgba(240, 187, 162, 0.5) 85%, rgba(197, 173, 145, 1) 100%);
        border-radius: 50% / 0% 0% 80% 80%;
    }

    .lead {
        position: relative;
        top: -14px;
        left: 3px;
        width: 0;
        height: 0;
        border-top: solid 13px #000000;
        border-right: solid 7px rgba(255, 255, 255, 0);
        border-left: solid 7px rgba(255, 255, 255, 0);
        z-index: 1;
    }

    .lead:before {
        position: absolute;
        content: "";
        top: -13px;
        left: -5px;
        border-top: solid 10px rgba(255, 255, 255, .6);
        border-right: solid 0 rgba(0, 255, 0, 0);
        border-left: solid 5px rgba(255, 255, 255, 0);
    }

    #pencil_wrapper.green .shaft {
        background-color: #3a3a3a;
        border-right: solid 4px black;
        border-bottom: solid 6px black;
    }

    #pencil_wrapper.green .shaft:before {
        background-color: #3a3a3a;
        border-right: solid 4px black;
        border-bottom: solid 4px black;
        border-left: solid thin black;
    }

    #pencil_wrapper.green .shaft:after {
        background-color: #3a3a3a;
        border-right: solid 4px black;
        border-bottom: solid 4px black;
        border-left: solid thin black;
    }
</style>
