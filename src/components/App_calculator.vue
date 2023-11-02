<template >
    <div class="calculator">
        <div class="display">{{ current || '0'}}</div>
        <div @click="clear" class="btn">C</div>
        <div @click="sign" class="btn ">+/-</div>
        <div @click="percent" class="btn ">%</div>
        <div @click="divide" class="btn oparetor">/</div>

        <div @click="append(7)" class="btn">7</div>
        <div @click="append(8)"  class="btn">8</div>
        <div @click="append(9)" class="btn">9</div>
        <div @click="times" class="btn oparetor">x</div>

        <div @click="append(4)"  class="btn">4</div>
        <div @click="append(5)"  class="btn">5</div>
        <div @click="append(6)"  class="btn">6</div>
        <div @click="minus" class="btn oparetor">-</div>

        <div @click="append(1)"  class="btn">1</div>
        <div @click="append(2)"  class="btn">2</div>
        <div @click="append(3)" class="btn">3</div>
        <div @click="add" class="btn oparetor">+</div>

        <div @click="append(0)" class="btn zero">0</div>
        <div @click="dot" class="btn ">.</div>
        <div @click="equal" class="btn oparetor">=</div>
       
    </div>
</template>

<script>


export default {
  data(){
    return{
        previous: null,
        current: '0',
        oparetor: null,
        oparetorClicked: false,
    }
  },
  methods: {
    clear(){
        this.current = '';
    },
    sign(){
        this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent(){
        this.current = `${parseFloat(this.current) / 100}`
    },
    append(number){
        if(this.oparetorClicked){
            this.current = '';
            this.oparetorClicked = false;
        }
        this.current =`${ this.current}${number}`;
    },
    dot(){
        if(this.current.indexOf('.') === -1){
            this.append('.');
        }
    },
    setPrivious(){
        this.previous = this.current;
        this.oparetorClicked = true;
    },
    divide(){
        this.oparetor = (a, b) => a / b;
        this.setPrivious();
    },
    times(){
        this.oparetor = (a, b) => a * b;
        this.setPrivious();

    },
    minus(){
        this.oparetor = (a, b) => a - b;
        this.setPrivious();

    },
    add(){
        this.oparetor = (a, b) => a + b;
        this.setPrivious();

    },
    equal(){
        this.current =`${this.oparetor(parseFloat(this.current), parseFloat(this.previous) )}`;
        this.previous = null;
    }

  }
}
</script>

<style scoped>
.calculator{
    width: 400px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(5px, auto);
}
.display{
    font-size: 40px;
    grid-column: 1/5;
    background:#333;
    color: #fff;
    cursor: text;
    padding: 15px;
}
.zero{
    grid-column: 1/3;
}
.btn{
    background-color: #f2f2f2; ;
    border: 1px solid #999;
    cursor: pointer;
    padding: 20px 8px;
    font-size: 24px;
}
.oparetor{
    background-color: orange ;
    color: #fff;
}

</style>
