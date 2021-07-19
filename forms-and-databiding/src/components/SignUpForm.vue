<template>
<div>
    <form @submit.prevent="handleSubmit">
        <label>Email: </label>
        <input type="email" required v-model="email">
        
        <!-- O v-model é um Two way data biding ou seja ele altera e registra o dado (data) dinamicamente quando referenciado no input. -->
     
        <label>Password: </label>
        <input type="password" required v-model="password">
        <div v-if="passwordError">{{passwordError}}</div>
     
        <label>Role:</label>
        <select v-model="role">
            <!-- O v-model quando temos um dropdown select é no proprio select e ele vai retornar o value. -->
            <option value="Developer">Web Developer</option>
            <option value="Designer">Web Designer</option>
        </select>

        <div class="terms">
            <input type="checkbox" v-model="terms">
            <label>Acept terms and conditions</label>
        </div>

    <div>
        <input type="checkbox" value="Shaun" v-model="names">
        <label>Shaun</label>
    </div>
       <div>
        <input type="checkbox" value="Yoshi" v-model="names">
        <label>Yoshi</label>
    </div>
       <div>
        <input type="checkbox" value="Mario" v-model="names">
        <label>Mario</label>
    </div>

    <label>Skills: </label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{skill}}</span>
        <!-- quando em um evento passamos uma função com parametro esse parametro vai ser o que disparar o evento como por exemplo 
        o objet clicado que vai ser o parametro a ser passado na função. -->
    </div>

    <div>
    <button class="submit">Create Acount</button>
    </div>

    </form>

        
    <p>{{email}}</p>
    <p>{{password}}</p>
    <p>{{role}}</p>
    <p>{{terms}}</p>
    <p>Names: {{names}}</p>



</div>
</template>

<script>
export default {
  data(){
    return {
        email: '',
        password: '',
        role: 'Designer',
        terms: false,
        names: [], //quando temos um checkbox multiplo nos devemos setar o valor o dado (data) deverá ser um array, o v-model será igual 
        //em todos os checkboxes que irão inputar o value nesse array.
        tempSkill: '',
        skills: [],
        passwordError: ''
        //aqui estamos declarando o valor default pelo Value do form, pois o v-model é um two way biding ou seja os dados sempre serão o mesmo independente
        //de onde ele for atualizado.
    }
  },
  methods: {
      addSkill(e){
          if(e.key === ',' && this.tempSkill) { //o this.tempSkill está indicando se há algum valor nesse dado é um boolean.
            if(!this.skills.includes(this.tempSkill)){ //O includes verifica se um elemento está incluso retornando true em um array. Quando declaramos a diferença significa que ele vai retornar falso e não vai executar o nosso if.
              this.skills.push(this.tempSkill) //aqui estamos usando o push() func raiz do js que joga um valor para um array no caso o tempSkill.
            }
              this.tempSkill = '' //vai limpar o campo do input. 
          }
      },
      deleteSkill(skill){
          this.skill = this.skills.filter((item) => {
              return skill !== item
          })
      },
      handleSubmit(){
          console.log('Form Submited')
          this.passwordError = this.password.lenght < 5 ? '' : 'Password must be at least 6 chart long'
          if (!this.passwordError) {
              console.log('Form Sended')
          }
      }
  }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px; 
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555

    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
</style>