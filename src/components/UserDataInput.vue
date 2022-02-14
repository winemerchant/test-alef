<template>
    <div class="container-input">
        <h3>Персональные данные</h3>
        <button v-on:click='clearLocaleStorage'> Очистить кэш </button>
        <div class="card-input">
            <label for='username' class='username'> Имя </label>
            <input class='user-name' id='username' type='text' v-model='name'/>
            <label for='userage' class='userage'> Возраст </label>
            <input class='user-age' id='userage' type='text' v-model='age'/>
        </div>
        <div class="card-child-input">
            <h3>Дети</h3>
            <UserChildren v-on:send='sendChild'/>
            <button class='save-btn' v-on:click='save'> Сохранить </button>
        </div>
    </div>
</template>

<script>
import UserChildren from './UserChildren.vue'

export default {
    components: {
        UserChildren
    },
    data() {
        return {
            name: '',
            age: '',
            children: []
        }
    },
    mounted() {
        if (localStorage.getItem('name')) {
            try {
                this.name = JSON.parse(localStorage.getItem('name'))
            } catch(Error) {
                localStorage.removeItem('name')
            }
        }
        if (localStorage.getItem('age')) {
            try {
                this.age = JSON.parse(localStorage.getItem('age'))
            } catch(Error) {
                localStorage.removeItem('age')
            }
        }
    },
    methods: {
        save() {
            this.$emit('save', {
                name: this.name,
                age: this.age,
                children: this.children
            })
            this.saveToLocalStorage()
            
        },

        sendChild(data) {
            this.children = data
        },
        saveToLocalStorage() {
            const parsedName = JSON.stringify(this.name)
            const parsedAge = JSON.stringify(this.age)
            localStorage.setItem('name', parsedName)
            localStorage.setItem('age', parsedAge)
        },
        clearLocaleStorage() { 
            localStorage.removeItem('name')
            localStorage.removeItem('age')
            location.reload()
        }
    }
}
</script>

<style>
.container-input {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 0px;
    width: 616px;
    height: 166px;
    position: relative;
    left: 375px;
    top: 30px;
}

.card-input {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 0px;
    position: relative;
    width: 616px;
    height: 122px;
    left: 0px;
    top: 44px;
}

.card-child-input {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 0px;
    position: relative;
    width: 616px;
    height: 166px;
    left: 0px;
    top: 88px;
}

.save-btn {
display: flex;
flex-direction: column;
align-items: center;
padding: 10px 20px;
position: relative;
width: 118px;
height: 44px;
left: 0px;
top: 30px;
color: white;
background: #01A7FD;
border-radius: 100px;
}

.user-name, .user-age {
    width: 616px;
    height: 56px;
    margin-top: 5px;
    font-family: Arial, Helvetica, sans-serif;
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 171% */

    display: flex;
    align-items: center;

    /* Colors / Black */

    color: #111111;
}

.username {
    position: absolute;
    top: 2px;
    left: 4px;
    
    font-style: normal;
    font-weight: normal;
    font-size: 13px;
    display: flex;
    align-items: center;
    color: rgba(17, 17, 17, 0.48);
    
}

.userage {
    position: absolute;
    top: 64px;
    left: 4px;
    font-style: normal;
    font-weight: normal;
    font-size: 13px;
    display: flex;
    align-items: center;
    color: rgba(17, 17, 17, 0.48);
}

</style>