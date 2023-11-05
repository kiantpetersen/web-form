<template>
  <form @submit.prevent="handleSubmit" class="form">
    <label>Email: </label>
    <input type="email" required v-model="email"/>
    <label>Password: </label>
    <input type="password" required v-model="password"/>
<label>Role:</label>
<select v-model="role">
    <option selected value="developer">Web Developer</option>
    <option value="designer">Web Designer</option>
</select>
<label>Skills:</label>
<input type="text" v-model="tempSkill" @keyup.alt="addSkill">
<div  v-for="skill in skills" :key="skill">
    <span @click="deleteSkill(skill)">

        {{skill}}
    </span>
</div>

<div class="terms">
    <input v-model="terms" type="checkbox" required/>
    <label> Accept all terms and conditions</label>
</div>
<!-- <div >
    <input type="checkbox" value="shaun" v-model="names"/>
    <label>Shaun</label>
</div>
<div >
    <input type="checkbox" value="peter" v-model="names"/>
    <label>Peter</label>
</div>
<div >
    <input type="checkbox" value="sarah" v-model="names"/>
    <label>Sarah</label>
</div> -->
<div class="submit">
    <button>Submit Form</button>
</div>
</form>
<p v-if="passwordErr.length">{{ passwordErr }}</p>
<p>Email:{{ email }}</p>
<p>Password:{{ password }}</p>
<p>Role:{{ role }}</p>
<p>Terms:{{ terms }}</p>
<!-- <p>Names:{{ names }}</p> -->
</template>

<script>
export default {
    data(){
        return{
            email:'',
            password:'',
            role:'developer',
            terms:false,
            tempSkill:'',
            skills:[],
            passwordErr:'',
            // names:[]
        }
    },
    methods:{
        addSkill(e){
          if ( e.key===',' && this.tempSkill ){
            if (!this.skills.includes(this.tempSkill)){

                this.skills.push(this.tempSkill)
            }
            this.tempSkill=''
          }
        },
        deleteSkill(skill){
            this.skills=this.skills.filter(item=>{
                return skill!==item

            })
        },
        handleSubmit(){
            console.log('form submitted')
            this.passwordErr=this.password.length>5?'':'Password is too short'
            if (!this.passwordErr){
                console.log(this.data)
            }
        }
    }

}
</script>

<style>
.form{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;;
}

</style>