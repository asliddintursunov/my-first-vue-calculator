<template>
    <div id="container">
        <div class="calculator-top"></div>
        <div>
            <div class="output-container">
                <input type="text" v-model="current" placeholder="0">
            </div>
            <div class="main-container">
                <button type="button" v-for="elem in main" :key="elem" @click="mains(elem)">{{ elem }}</button>
            </div>
            <div class="btn-arithmetic-container">
                <div class="nums-container">
                    <button type="button" v-for="nums in numbers" :key="nums" @click="display(nums)">{{ nums }}</button>
                    <button v-if="dot" @click="point">{{ dotValue }}</button>
                    <button v-else>{{ dotValue }}</button>
                </div>
                <div class="arithmetic-container">
                    <template v-for="arif in arithmetics" :key="arif">
                        <button type="button" v-if="arithIsTrue" @click="showAriths(arif)">{{ arif }}</button>
                        <button type="button" v-else >{{ arif }}</button>
                    </template>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            dot: true,
            dotValue: '.',
            numbers: ['=', 0, 3, 2, 1, 6, 5, 4, 9, 8, 7,].reverse(),
            arithIsTrue: true,
            arithmetics: ['+', '-', '*', '/'],
            main: ['AC', '%', '+/-', '↩'],
            current: '',
        }
    },
    methods: {
        display(value){
            if(value !== this.numbers[this.numbers.length - 1]){
                this.current += value
            }else{
                this.current = eval(this.current).toFixed(1)
                if (this.dot = false) {
                    this.dot = true
                } else {
                    this.dot = false
                }
            }

            this.arithIsTrue = true
            
        },
        showAriths(value){
            if(this.current.length < 1){
                this.current = ''
            }else{
                this.current += value
                if (this.current.includes(value)) {
                    this.arithIsTrue = false
                }
                else{
                    this.arithIsTrue = true
                }
            }
            if (value === this.arithmetics[0] || value === this.arithmetics[1] || value === this.arithmetics[2] || value === this.arithmetics[3]) {
                this.dot = true
            }
        },
        point(){
            if(this.current.length < 1){
                this.current = ''
            }else{
                this.dot = false
                this.current += this.dotValue
            }
        },

        mains(value){
            if (value === this.main[0]) {
                this.current = ''
                this.arithIsTrue = true
                this.dot = true
            }
            if (value === this.main[1]) {
                this.current = eval(this.current).toFixed(1)
                this.current = this.current / 100
            }
            if (value === this.main[2]) {
                this.current = eval(this.current).toFixed(1)
                this.current = this.current / (-1)
            }
            if (value === this.main[3]) {
                let x = this.current.split('')
                x.pop()
                this.current = x.join('')
            }
        }
    },
    
}
</script>
<style scoped>
    #container{
        display: flex;
        flex-direction: column;
        user-select: none;
        padding: 1.7rem 1rem 1.5rem 1rem;
        background-color: lightblue;
        border: none;
        border-radius: 1rem;
    }
    input{  
        padding: 0.3rem 0rem;
        border-radius: 0.3rem;
        outline-width: 0;
        text-align: right;
    }
    button{
        padding: 0.5rem 1.2rem;
        margin: 0.2rem;
        color: white;
        border: none;
        cursor: pointer;
        border-radius: 0.5rem;
    }
    button:hover{
        opacity: 0.8;
    }
    button:active{
        opacity: 0.9;
    }
    .nums-container button{
        background-color: rgb(97, 97, 97);
    }
    .arithmetic-container button{
        background-color: orange;
    }
    .main-container button{
        background-color: rgb(157, 157, 157);
    }
    .calculator-top{
        width: 5rem;
        height: 0.2rem;
        border-radius: 3rem;
        background-color: black;
        margin-bottom: 2rem;
    }
</style>
