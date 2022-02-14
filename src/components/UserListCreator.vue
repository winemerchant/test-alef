<template>
    <div class="card-output">
        <button v-on:click='clearLocaleStorage'> Очистить кэш </button>
         <div class="card-user">
            <h3> Персональные данные </h3>
            <p> {{user.name}}, {{user.age}} </p>
        </div>
        <div class="card-child">
            <h3> Дети </h3>
            <ul>
                <li v-for='child in children' v-bind:key='child.id'>
                    {{child.name}}, {{child.age}}
                </li>
            </ul>
        </div>
        <div v-if='seen'> <UserDataList v-on:refresh='importData'/> </div>
    </div>
</template>


<script>
import UserDataList from './UserDataList.vue'

export default {
    components: {
        UserDataList
    },
    data() {
        return {
            user: '',
            children: [],
            seen: false
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
        importData(data) {
            this.user = data.user
            this.children = data.children
            console.log('it works')
            this.saveToLocalStorage()
        },
        saveToLocalStorage() {
            const parsed = JSON.stringify(this.user, this.children)
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
    // props: ['user', 'children']
}
</script>

<style>
.card-output {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 0px;

    position: absolute;
    width: 197px;
    height: 280px;
    left: 375px;
    top: 30px;
}

p, li {
    font-family: Arial, Helvetica, sans-serif;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    color: #111111;

}

ul, li {
    list-style-type:none;
    margin-left: 0; 
    padding-left: 0
}

li {
display: flex;
flex-direction: column;
justify-content: center;
align-items: flex-start;
padding: 10px 20px;
margin-bottom: 20px;

position: static;
width: 143px;
height: 44px;
left: 0px;
top: 44px;

/* Colors / GrayL */

background: #F1F1F1;
border-radius: 5px;
}
</style>