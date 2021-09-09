<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Cálculo IMC!</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content>
 
        <ion-grid>
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
              <ion-input inputmode="numeric" type="number" id="altura" v-model.number="altura" clear-on-edit="true"></ion-input>
            </ion-col>
          </ion-row>
          
          <!--Inserção de peso -->
          <ion-row>
            <ion-col>
              <ion-label>Peso:</ion-label>
              <ion-input inputmode="numeric" type="number" id="peso" v-model.number="peso" clear-on-edit="true"></ion-input>
            </ion-col>
          </ion-row>

          <!--Botão para realização do cálculo IMC-->
          <ion-row>
            <ion-col>
              <ion-button @click="calcularIMC()" expand="block">Calcule IMC!</ion-button>
            </ion-col>
          </ion-row>

          <!-- Coluna para mostra de resultados-->
          <ion-row >
            <ion-col>
              <ion-textarea v-if="calculado" type="text" id="mensagem" v-model="mensagem"></ion-textarea>
            </ion-col>            
          </ion-row>

          <!--Botão para atualização de página-->
          <ion-row>
            <ion-col>
              <ion-button v-if="calculado" @click="atualizarPagina()">Novo cálculo</ion-button>
            </ion-col>
          </ion-row>
            
        </ion-grid>

    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol, IonLabel, IonInput, IonButton, IonTextarea } from '@ionic/vue';
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
    IonTextarea,
  },
  data(){
    return{
      nome:'',
      altura:0,
      peso:0,
      mensagem:'',
      calculado:false, //variavel para definir se o calculo já foi feito para mostra de resultados
    }
  },
  methods:{
    //Cálculo do IMC e criação da mensagem de retorno se baseando em tabela do site programasaudefacil
    async calcularIMC(){
      const IMC=this.peso/(this.altura*this.altura);
      if (IMC<18.5){
        this.mensagem = 'Seu IMC é: '+IMC+'\nVoce está classificado com Magreza'
      }else if (IMC<24.9){
        this.mensagem = 'Seu IMC é: '+IMC+'\nVoce está classificado com IMC Normal'        
      }else if (IMC<29.9){
        this.mensagem = 'Seu IMC é: '+IMC+'\nVoce está classificado com Sobrepeso'        
      }else if (IMC<39.9){
        this.mensagem = 'Seu IMC é: '+IMC+'\nVoce está classificado com Obesidade'        
      }else {
        this.mensagem = 'Seu IMC é: '+IMC+'\nVoce está classificado com Obesidade II'        
      }
      this.calculado=true;
    },
    atualizarPagina(){
      window.location.reload()
    },
  },
  
});
</script>

<style scoped>
ion-input{
  border:solid 2px black;
  background: black;
  border-radius: 10px;
  --placeholder-color:white;
  color:white;
  font-size: 15px;
}
ion-title{
  font-size: 24px;
  font-weight: 700;
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