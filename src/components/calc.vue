<template>
  <div class="calc">

    <div class="visor">{{ visor }}</div>
    <div class="btn" @click="calcular('acao', 'AC')">AC</div>
    <div class="btn" @click="calcular('acao', '+/-')">+/-</div>
    <div class="btn" @click="calcular('acao', '%')">%</div>
    <div class="btn operador" @click="calcular('acao', '/')">/</div>
    
    <div class="btn" @click="calcular('valor', '7')">7</div>
    <div class="btn" @click="calcular('valor', '8')">8</div>
    <div class="btn" @click="calcular('valor', '9')">9</div>
    <div class="btn operador"  @click="calcular('acao', '*')">*</div>
    
    <div class="btn" @click="calcular('valor', '4')">4</div>
    <div class="btn" @click="calcular('valor', '5')">5</div>
    <div class="btn" @click="calcular('valor', '6')">6</div>
    <div class="btn operador" @click="calcular('acao', '-')">-</div>
    
    <div class="btn" @click="calcular('valor', '1')">1</div>
    <div class="btn" @click="calcular('valor', '2')">2</div>
    <div class="btn" @click="calcular('valor', '3')">3</div>
    <div class="btn operador" @click="calcular('acao', '+')">+</div>
    
    <div class="btn" @click="calcular('valor', '0')">0</div>
    <div class="btn" @click="calcular('valor', '00')">00</div>
    <div class="btn" @click="calcular('acao', '.')">.</div>
    <div class="btn operador" @click="calcular('acao', '=')">=</div>
    

  </div>
  
</template>

<script>
export default {
  
  data(){
    return{
      visor: '0',
      ope: null
    }
  },
  methods:{
    
    calcular(tipo, valor){
      if(this.visor == '0' || this.ope){
        this.visor = ''
        this.ope = null
      }

      if(tipo === 'acao' ){
        
        if(valor == 'AC') this.limpar()
        if
        (valor == '+' || valor == '-' || valor == '/' || valor == '*' ||  valor == '-'){
          this.visor+=valor
        }

        if(valor == '.') this.visor += '.'
        if(valor == '+/-') this.sinal()
        if(valor == '%') this.porcento()
        if(valor == '=') {
          this.visor = eval(this.visor)
          this.ope = true
        }

      }else if(tipo === 'valor'){
        this.visor += valor
      }
    },

    limpar(){
      this.visor = '0'
    },

    sinal(){
      this.visor = this.visor.charAt(0) == '-' ? 
        this.visor.slice(1) : `-${this.visor}`
    },
    porcento(){
      this.visor = `${parseFloat(this.visor) / 100}`
    }    
        
  }
}
</script>

<style scoped>

.calc{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);  
  font-size: 40px;
  width: 400px;
  text-align: center;
  margin: 15% auto;
  
}
.visor{
  grid-column: 1/5;
  text-align: center;
  background: transparent;
  border-radius: 15px;  
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  text-shadow: gray 2px 3px;
  letter-spacing: 2px;  
  width: 400px;
  border: solid 5px;
}

.btn{
  background: black;
  color: #fff;
  border: 1px solid #fff;  
}
.btn:hover{
  transform: translateY(1px);
}

.operador{
  background: red;
  color: #fff;
}


</style>
