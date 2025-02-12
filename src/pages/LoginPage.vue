<script setup lang="ts">
    import {reactive, ref,computed,watch} from 'vue'

    const data = reactive({
        email:'',
        password:''
    })
    const isValid = ref(false)


    watch(data, (val)=>{
        console.log('Changement dans la varibale')
    })

    //Changement de la valeur pour afficher le submit
    watch([() => data.email,()=> data.password],()=>{
        if (isUserInputEmailValid(data.email) && isUserInputPasswordValid(data.password)){
            isValid.value=true
        }
        else{
            isValid.value=false
        }
    })

    //Vérification de l'email
    const isUserInputEmailValid = (input:string):boolean => {
        const pattern = new RegExp(/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/)
        return pattern.test(input)
    }

    //Vérification du password
    const isUserInputPasswordValid = (input:string):boolean => {
        const pattern = new RegExp(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*])[A-Za-z\d!@#$%^&*]{8,}$/)
        return pattern.test(input)
    }

    const submitHandler = () => {

    }

    const resetHandler = () => {
        data.email=""
        data.password=""
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
                    :disabled="!isValid"
                >Submit</button>
                <button 
                    type="reset"
                    class="button is-danger"
                    @click="resetHandler"
                >Reset</button>
            </section>
        </form>
    </main>
</template>

<style lang="scss" scoped>
.login_main{

}
</style>