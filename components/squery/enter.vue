<template>
    <div>
        <div class="squery-wrap">
            <div class="bg"></div>
            <div class="li"></div>
        </div>
    </div>
</template>

<script setup lang=ts>
import { ref, reactive } from 'vue';
import { FORMATS } from '~/static/js/pixi.mjs';
class sli {
    constructor(classname: any, size = 10) {
        this.size = size;
        this.classname = classname;
        this.c = null;
    }
    work() {
        console.log("我们会一直跑");
    }
    create() {
        if (process.client) {
            const c = document.createElement('div');
            c.setAttribute('class', this.classname);
            c.setAttribute('style', "left: 40px;top:60px;background: #f0f;width: 10px;height: 10px;position: absolute;");
            this.c = c;
        }
    }
    run() {
        this.create();
    }
    hold() {
        this.run();
        return this.c;
    }
    getName() {
        return this.surname + this.name
    }
}
class pan {
    constructor(classname: any, psum = 2) {
        this.psum = psum;
        this.classname = classname;
    }
    work() {
        console.log("我们会一直跑");
    }
    createP() {
        if (process.client) {
            for (let i = 0; i < this.psum; i++) {
                const newli = new sli('li', 10).hold();
                nextTick(()=>{
                    document.querySelector(this.classname).appendChild(newli);
                })
            }
        }

    }
    getName() {
        return this.surname + this.name;
    }
}
const game: any = new pan('.squery-wrap',3);
game.createP();
</script>

<style lang='scss' scoped>
.squery-wrap {
    display: inline-block;
    width: 600px;
    height: 600px;
    background: #eee;
    position: relative;

    .li {
        display: inline-block;
        width: 10px;
        height: 10px;
        position: absolute;
        left: 20px;
        top: 50px;
        background: #f0f;
    }
}
</style>