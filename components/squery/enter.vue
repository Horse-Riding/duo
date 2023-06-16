<template>
    <div>
        <div class="squery-wrap">
            <div class="bg"></div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive } from 'vue';
import { FORMATS } from '~/static/js/pixi.mjs';
// 设置颜色
const setColor = () => {
    const r = Math.floor(Math.random() * 256);
    const g = Math.floor(Math.random() * 256);
    const b = Math.floor(Math.random() * 256);
    return `rgb(${r},${g},${b})`;
}
class sli {
    constructor(classname, size = 10, maxRange = 1000) {
        this.size = size;
        this.classname = classname;
        this.c = null;
        this.pl = 0;
        this.pt = 0;
        this.color = setColor();
        this.maxRange = (maxRange / this.size) - 1;
    }

    // 出生地点
    setBirsthPosition() {
        let newPort = () => {
            console.log(this.maxRange);
            return Math.round(Math.random() * this.maxRange);
        }
        this.pl = newPort();
        this.pt = newPort();
        // 是否在行动
        this.runstate = null;
        console.log(this.pl);
        console.log(this.pt);
    }
    move() {
        let event = Math.round(Math.random() * 4);
        switch (event) {
            // 停留
            case 0:
                break;
            // 左
            case 1:
                if (this.pt > 0) {
                    this.pt -= 1;
                }
                break;
            // 上
            case 2:
                if (this.pl > 0) {
                    this.pl -= 1;
                }
                break;
            // 右
            case 3:
                if (this.pl < this.maxRange) {
                    this.pl += 1;
                }
                break;
            // 下
            case 4:
                if (this.pt < this.maxRange) {
                    this.pt += 1;
                }
                break;
            // 停留
            default:
                break;
        }
        this.draw();
    }
    // 绘制位置
    draw() {
        nextTick(() => {
            this.c.setAttribute('style', `left: ${this.pl * this.size}px;top:${this.pt * this.size}px;background: ${this.color};width: 10px;height: 10px;position: absolute;`);
        })
    }
    work() {
        this.runstate = setInterval(() => {
            this.move();
        }, 1000)
    }
    create() {
        if (process.client) {
            this.setBirsthPosition();
            const c = document.createElement('div');
            c.setAttribute('class', this.classname);
            c.setAttribute('style', `left: ${this.pl * this.size}px;top:${this.pt * this.size}px;background: ${this.color};width: 10px;height: 10px;position: absolute;`);
            this.c = c;
        }
        this.work();
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
    constructor(classname, psum = 10) {
        this.psum = psum;
        this.classname = classname;
    }
    work() {
        console.log("我们会一直跑");
    }
    createP() {
        if (process.client) {
            for (let i = 0; i < this.psum; i++) {
                const newli = new sli('li', 10, 600).hold();
                nextTick(() => {
                    document.querySelector(this.classname).appendChild(newli);
                })
            }
        }
    }
    getName() {
        return this.surname + this.name;
    }
}
const game = new pan('.squery-wrap', 20);
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