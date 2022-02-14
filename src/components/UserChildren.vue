<template>
    <div class="card">
        <div class="input-string" v-if="childrenInputes[0]['seen']" v-on:input='send'>
            <label for='childname' class='childname'> Имя </label>
            <input class='child-name' id='childname' type='text' v-model="childrenInputes[0]['name']"/>
            <label for='childage' class='childage'> Возраст </label>
            <input class='child-age' id='childage' type='text' v-model="childrenInputes[0]['age']"/>
            <button class='del-btn' v-on:click="del1"> Удалить </button>
        </div>
        <div class="input-string" v-if="childrenInputes[1]['seen']" v-on:input='send'>
            <label for='childname' class='childname'> Имя </label>
            <input class='child-name' id='childname' type='text' v-model="childrenInputes[1]['name']"/>
            <label for='childage' class='childage'> Возраст </label>
            <input class='child-age' id='childage' type='text' v-model="childrenInputes[1]['age']"/>
            <button class='del-btn' v-on:click="del2"> Удалить </button>
        </div>
       <div class="input-string" v-if="childrenInputes[2]['seen']" v-on:input='send'>
           <label for='childname' class='childname'> Имя </label>
            <input class='child-name' id='childname' type='text' v-model="childrenInputes[2]['name']"/>
            <label for='childage' class='childage'> Возраст </label>
            <input class='child-age' id='childage' type='text' v-model="childrenInputes[2]['age']"/>
            <button class='del-btn' v-on:click="del3"> Удалить </button>
        </div>
        <div class="input-string" v-if="childrenInputes[3]['seen']" v-on:input='send'>
            <label for='childname' class='childname'> Имя </label>
            <input class='child-name' id='childname' type='text' v-model="childrenInputes[3]['name']"/>
            <label for='childage' class='childage'> Возраст </label>
            <input class='child-age' id='childage' type='text' v-model="childrenInputes[3]['age']"/>
            <button class='del-btn' v-on:click="del4"> Удалить </button>
        </div>
        <div class="input-string" v-if="childrenInputes[4]['seen']" v-on:input='send'>
            <label for='childname' class='childname'> Имя </label>
            <input class='child-name' id='childname' type='text' v-model="childrenInputes[4]['name']"/>
            <label for='childage' class='childage'> Возраст </label>
            <input class='child-age' id='childage' type='text' v-model="childrenInputes[4]['age']"/>
            <button class='del-btn' v-on:click="del5"> Удалить </button>
        </div>
        <div v-if='addseen'> <button v-on:click='showNewInput' class='add-btn'> Добавить ребенка </button> </div>
         <button v-on:click='clearLocaleStorage'> Очистить кэш </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            
            key: 0,
            childrenInputes: [
                {seen: false, name: null, age: null},
                {seen: false, name: null, age: null},
                {seen: false, name: null, age: null},
                {seen: false, name: null, age: null},
                {seen: false, name: null, age: null}
            ],
            children: [],
            addseen: true    
        }
    },
    updated() {
        this.showAddButton()
    },
    mounted(){
        if (localStorage.getItem('childrenInputes')) {
            try {
                this.childrenInputes = JSON.parse(localStorage.getItem('childrenInputes'))
            } catch(Error) {
                localStorage.removeItem('childrenInputes')
            }
        }
         if (localStorage.getItem('key')) {
            try {
                this.key = JSON.parse(localStorage.getItem('key'))
            } catch(Error) {
                localStorage.removeItem('key')
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
        showNewInput() {
            if(this.key <= 4) {
                this.childrenInputes[this.key]['seen'] = true
                console.log(this.key)
                this.showAddButton()
                this.key++
            }
        },
        send() {
            this.children = []
            for (let child of this.childrenInputes) {
                if(child.seen == true && child.name != null && child.age != null ) {
                    this.children.push(child)
                }
            }
            this.$emit('send', this.children)
            this.saveToLocalStorage()
        },

        saveToLocalStorage() {
            const childrenInputes = JSON.stringify(this.childrenInputes)
            const key = JSON.stringify(this.key)
            const children = JSON.stringify(this.children)
            localStorage.setItem('childrenInputes', childrenInputes)
            localStorage.setItem('key', key)
            localStorage.setItem('children', children)
            },
        clearLocaleStorage() {
            localStorage.removeItem('childrenInputes')
            localStorage.removeItem('key')
            localStorage.removeItem('children')
            location.reload()
        },
        del1() {
            this.childrenInputes[0]['seen'] = false
            this.childrenInputes[0]['name'] = null
            this.childrenInputes[0]['age'] = null
            this.key -- 
            this.saveToLocalStorage()
            this.send()
        
        },
        del2() {
            this.childrenInputes[1]['seen'] = false
            this.childrenInputes[1]['name'] = null
            this.childrenInputes[1]['age'] = null
            this.key -- 
            this.saveToLocalStorage()
            this.send()
            
        },
        del3() {
            this.childrenInputes[2]['seen'] = false
            this.childrenInputes[2]['name'] = null
            this.childrenInputes[2]['age'] = null
            this.key -- 
            this.saveToLocalStorage()
            this.send()
            
        },
        del4() {
            this.childrenInputes[3]['seen'] = false
            this.childrenInputes[3]['name'] = null
            this.childrenInputes[3]['age'] = null
            this.key -- 
            this.saveToLocalStorage()
            this.send()
            
        },
        del5() {
            this.childrenInputes[4]['seen'] = false
            this.childrenInputes[4]['name'] = null
            this.childrenInputes[4]['age'] = null
            this.key -- 
            this.saveToLocalStorage()
            this.send()
            
        },
        showAddButton() {
            if (this.key == 5) {
                this.addseen = false
            }
            if (this.key < 5) {
                this.addseen = true
            }
        }
    }
}
</script>

<style>

.add-btn{
    display: flex;
flex-direction: column;
align-items: center;
padding: 10px 20px;

position: absolute;
width: 204px;
height: 44px;
left: 460px;
top: 1px;

border: 2px solid #01A7FD;
box-sizing: border-box;
border-radius: 100px;
}

.child-name, .child-age {
    width: 260px;
    height: 56px;
}

.del-btn {
    position: relative;
    width: 60px;
    height: 24px;
    left: 18px;
    top: 0px;
    font-family: Montserrat;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    color: #01A7FD;
}
.input-string {
    position: relative;
}
.childname {
    position: absolute;
    top: 1px;
    left: 3px;
    font-style: normal;
    font-weight: normal;
    font-size: 13px;
    display: flex;
    align-items: center;
    color: rgba(17, 17, 17, 0.48);
}

.childage {
    position: absolute;
    top: 1px;
    left: 271px;
    font-style: normal;
    font-weight: normal;
    font-size: 13px;
    display: flex;
    align-items: center;
    color: rgba(17, 17, 17, 0.48);
}
</style>