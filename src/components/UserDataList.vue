<template>
    <div class="container">
        
        <div class="card">
            <UserDataInput v-on:save='saveData' />
            
        </div>
        
        
        <!-- <div class="card">
            <h2> Данные пользователя </h2>
            <p> {{user.name}}, {{user.age}} </p>
        </div> -->
        <!-- <div class="card">
            <h2> Дети </h2>
            <ul>
                <li v-for='child in children' v-bind:key='child.id'>
                    {{child.name}}, {{child.age}}
                </li>
            </ul>
        </div> -->
        <!-- <UserListCreator v-bind:user='user' v-bind:children='children'/> -->
    </div>
</template>

<script>

import UserDataInput from './UserDataInput.vue'
// import UserListCreator from './UserListCreator.vue'

export default {
    components: {
        UserDataInput,
        // UserListCreator
    },
    // props: ['importData'],
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
            // console.log(this.children[0]['name'])

        },
         saveToLocalStorage() {
            const parsed = JSON.stringify(this.user)
            const parsenChildren = JSON.stringify(this.children)
            localStorage.setItem('user', parsed)
            localStorage.setItem('children', parsenChildren)
        },
        clearLocaleStorage() { //очищает LocaleStorage и обновляет страницу
            localStorage.removeItem('user')
            localStorage.removeItem('children')
            location.reload()
        }

        
    }
}
</script>