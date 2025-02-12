<script setup lang="ts">
    import {reactive, ref,computed,watch} from 'vue'
    import {useRouter} from 'vue-router'

    const router = useRouter()

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
        const pattern = new RegExp(/^(?!.*@.*@)(?!.*\..*\..*)[a-zA-Z0-9._%+-]{1,64}@[a-zA-Z0-9.-]{1,15}\.[a-zA-Z]{2,10}$/)
        return pattern.test(input)
    }

    //Vérification du password
    const isUserInputPasswordValid = (input:string):boolean => {
        const pattern = new RegExp(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*])[A-Za-z\d!@#$%^&*]{8,}$/)
        return pattern.test(input)
    }

    const submitHandler = async() => {

        const result = await fetch('users.json')
        const users = await result.json()
        console.log(users)

        const user = users.find((user:{ email:string,password:string}) => user.email === data.email)
        if(!user){
            alert('user not found')
            return
        }
        if(!(user.password===data.password)){
            alert('Wrong password')
            return
        }    

        router.push('session/' + user.id)
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