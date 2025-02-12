<script setup lang="ts">
    import {reactive, ref,computed,watch} from 'vue'

    const data = reactive({
        email:'',
        password:''
    })


    watch(data, (val)=>{
        console.log('Changement dans la varibale')
    })

    const isUserInputValid = (input:string):boolean => {
        const pattern = new RegExp(/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/)
        return pattern.test(input)
    }

    const submitHandler = () => {
        if (isUserInputValid(data.email)) {
            console.log('Email is valid')
        } else {
            console.log('Invalid email')
        }
    }

    const inputHandler = function(){
        
    }

</script>

<template>
    <main class="login_main">
        <h1>LoginPage</h1>

        <form @submit.prevent="submitHandler">
            <section>
                <article>
                    <label for="email">Email</label>
                    <input 
                        id="email" 
                        placeholder="Email"
                        type="email"
                        class="input"
                        v-model="data.email"
                        required/>
                </article>
                <article>
                    <label for="password">Password</label>
                    <input 
                        id="password"
                        placeholder="Password"
                        type="password"
                        class="input"
                        v-model="data.password"
                        required/>
                </article>
            </section>
            <section>
                <button 
                    type="submit"
                    class="button is-primary"
                >Submit</button>
                <button 
                    type="reset"
                    class="button is-danger"
                >Reset</button>
            </section>
        </form>
    </main>
</template>

<style lang="scss" scoped>
.login_main{

}
</style>