<template>
    <form @submit.prevent="submit">
        <label for="">Email</label>
        <input type="email" required v-model="email">

        <label for="">Password</label>
        <input type="password" required v-model="password">
        
        <div>
            <p class="error" v-if="errorMsg">{{errorMsg}}</p>
        </div>

        <label for="">Role</label>
        <select v-model="role">
            <option value="developer">Web developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <div>
            <label for="">Skills Press alt , to add new skill</label>
            <input type="text" @keyup.alt="addKey" v-model="skill">
        </div>
        <div v-for="skill in skills" :key="skill">
            <p class="todo-text">{{skill}} <span class="cross" @click="deleteSkill(skill)">&#x2716;</span></p>
        </div>
        <div>
            <button class="create">Create Account</button>
        </div>

        <!-- <label for="">Choose Names</label>
        <div>
            <input type="checkbox" v-model="accept">
            <label for="">Accept Terms and Condition</label>
        </div>

        <div>
            <input type="checkbox" value="psp" v-model="names">
            <label for="">Pyae Sone Paing</label>
        </div>
        <div>
            <input type="checkbox" value="hsu" v-model="names">
            <label for="">Hsu Latt</label>
        </div>
        <div>
            <input type="checkbox" value="mg" v-model="names">
            <label for="">Mg Mg</label>
        </div>
        <div>
            <input type="checkbox" value="kyaw" v-model="names">
            <label for="">Kyaw Gyi</label>
        </div> -->
    </form>
    <!-- <p>Email - {{email}}</p>
    <p>Password - {{password}}</p>
    <p>Role - {{role}}</p>
    <p>Accept - {{accept}}</p>
    <p>Skills - {{skills}}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: 'admin@gmail.com',
            password: '',
            role: 'designer',
            accept: false,
            skills: [],
            skill: '',
            errorMsg:''
        }
    },

    methods: {
        addKey(e) {
            if(e.key===',' && this.skill){
                this.skills.push(this.skill);
                this.skill = '';
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter(loopSkill=>{
                return loopSkill != skill;
            })
        },
        submit() {
            // Validation = form data thwy ko own create dh pr
            if(this.password.length < 8) {
                this.errorMsg = "Password must be at least 8 characters";
            } else {
                this.errorMsg = false
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background-color: #fff;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
        border: 10px 10px lightgrey;
    }

    label {
        color: #000;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.8em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }

    input,select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }

    input[type=checkbox] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }

    .cross {
        cursor: pointer;
        color: red;
        float: right;
    }

    .create {
        background-color: steelblue;
        padding: 15px 30px;
        color: #fff;
        border-radius: 10px;
        border: none;
        width: 100%;
        font-weight: bold;
        text-transform: uppercase;
        letter-spacing: 2px;
        margin: 10px 0 0 0;
    }

    button:active {
        color: #000;
        background-color: cyan;
    }

    .error {
        margin-right: 10px;
        color: crimson;
    }

    .todo-text {
        color: #000;
        font-weight: bold;
        font-size: 1em;
        text-transform: uppercase;
        letter-spacing: 1px;
    }
</style>