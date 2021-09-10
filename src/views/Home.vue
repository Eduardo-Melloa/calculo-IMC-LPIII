<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Cálculo IMC!</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content>
 
        <ion-grid v-if="!calculado">
          <form @submit.prevent="calcularIMC">
            <!--Inserção de nome  -->
            <ion-row>
              <ion-col>
                <ion-label>Nome:</ion-label>
                <ion-input type="text" id="nome" placeholder="Digite o seu nome" v-model="nome"></ion-input>
              </ion-col>
            </ion-row>

            <!--Inserção de altura -->
            <ion-row>
              <ion-col>
                <ion-label>Altura:</ion-label>
                <ion-input type="text" id="altura" v-model.number="altura" clear-on-edit="true" required></ion-input>
              </ion-col>
            </ion-row>
            
            <!--Inserção de peso -->
            <ion-row>
              <ion-col>
                <ion-label>Peso:</ion-label>
                <ion-input inputmode="numeric" type="number" id="peso" v-model.number="peso" clear-on-edit="true" required></ion-input>
              </ion-col>
            </ion-row>

            <!--Botão para realização do cálculo IMC-->
            <ion-row>
              <ion-col>
                <ion-button type="submit" expand="block">Calcule IMC!</ion-button>
              </ion-col>
            </ion-row>
          </form>
        </ion-grid>

        <ion-grid v-else>
        
          <!-- Coluna para mostra de resultados-->
          <ion-row>
            <ion-col>
              <ion-text color="secondary">
                <h1>{{ nome ? `${nome}, seu` : 'Seu' }} IMC é: {{ imc.toFixed(2) }}</h1>
                <h2>Voce está classificado como {{ classificacao }}</h2>
              </ion-text>
            </ion-col>            
          </ion-row>

          <!--Botão para atualização de página-->
          <ion-row>
            <ion-col>
              <ion-button @click="resetState">Novo cálculo</ion-button>
            </ion-col>
          </ion-row>
        </ion-grid>

    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol, IonLabel, IonInput, IonButton, IonText } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonGrid, 
    IonRow, 
    IonCol, 
    IonLabel, 
    IonInput, 
    IonButton, 
    IonText,
  },
  data(){
    return{
      nome: '',
      altura: undefined,
      peso: undefined,
      imc: undefined,
      classificacao: '',
      calculado: false, //variavel para definir se o calculo já foi feito para mostra de resultados
    }
  },
  methods:{
    //Cálculo do IMC e criação da mensagem de retorno se baseando em tabela do site programasaudefacil
    calcularIMC(){
      if (!this.peso || !this.altura) return;
      const imc = this.peso / (this.altura * this.altura);
      this.imc = parseFloat(imc);

      if (imc < 18.5) this.classificacao = 'Magreza';
      else if (imc < 24.9) this.classificacao = 'Normal';
      else if (imc < 29.9) this.classificacao = 'Sobrepeso';
      else if (imc < 39.9) this.classificacao = 'Obesidade';
      else this.classificacao = 'Obesidade II';

      this.calculado=true;
    },
    resetState(){
      this.nome = '';
      this.altura = undefined;
      this.peso = undefined;
      this.imc = undefined;
      this.classificacao = '';
      this.calculado = false;
    },
  },
  
});
</script>

<style scoped>
ion-grid {
  position: absolute;
  top: 50%;
  width: 100%;
  transform: translateY(-50%);
}
ion-input{
  border:solid 2px black;
  background: rgba(255, 255, 255, 0.082);
  border-radius: 10px;
  --placeholder-color:white;
  color:white;
  font-size: 15px;
}
ion-title{
  font-size: 24px;
  font-weight: 700;
  padding: 0;
}
ion-label{
  font-size: 18px;
  font-weight: 500;
}
ion-textarea{
  border:solid 2px black;
  border-radius: 10px;
}
</style>