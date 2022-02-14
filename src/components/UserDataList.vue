<template>
    <div class="container">
        
        <div class="card">
            <UserDataInput v-on:save='saveData' />
            
        </div>
    </div>
</template>

<script>

import UserDataInput from './UserDataInput.vue'

export default {
    components: {
        UserDataInput,
    },

    data() {
        return {
            countid: 0,
            user: {},
            children: []
        }
    },
    mounted() {
        if (localStorage.getItem('user')) {
            try {
                this.user = JSON.parse(localStorage.getItem('user'))
            } catch(Error) {
                localStorage.removeItem('user')
            }
        }
        if (localStorage.getItem('children')) {
            try {
                this.children = JSON.parse(localStorage.getItem('children'))
            } catch(Error) {
                localStorage.removeItem('children')
            }
        }
    },
    methods: {
        saveData(data) {
            this.user.name = data.name
            this.user.age = data.age
            this.children = data.children
            this.$emit(
                'refresh', {user: this.user, children: this.children}
            )
            this.saveToLocalStorage()


        },
         saveToLocalStorage() {
            const parsed = JSON.stringify(this.user)
            const parsenChildren = JSON.stringify(this.children)
            localStorage.setItem('user', parsed)
            localStorage.setItem('children', parsenChildren)
        },
        clearLocaleStorage() {
            localStorage.removeItem('user')
            localStorage.removeItem('children')
            location.reload()
        }

        
    }
}
</script>