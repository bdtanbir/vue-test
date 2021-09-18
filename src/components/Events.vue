<template>
    <div class="events-wrapper wrapper-box">
        <div :class="isLogin ? 'login' : 'hide-login login'">
            <p>Password: <strong>123</strong></p>
            <form @submit.prevent>
                <input type="password" v-model="loginPass" @keyup.enter="enteredPass">
                <button @click="enteredPass">Enter</button>
            </form>
            <p v-if="isWrongPass" class="wrong-pass">
                Your passwrod is invalid!
            </p>
        </div>
        <div class="quantity-box">
            <button @click="decrementBtn">-</button>
            <span class="quantity-number">{{quantityNum}}</span>
            <button @click="incrementBtn">+</button>
        </div>

        <button @click="showMultiStep" class="show-multistep-form">
            Show MultiSteps Form
        </button>

        <div class="select-model">
            <button @click="Multiselect">{{isMultiselect?'hide': 'show'}} Multiselect</button>
            <br/>
            <select v-model="selected" :multiple="isMultiselect">
                <option value="A">A</option>
                <option value="B">B</option>
                <option value="C">C</option>
            </select>
            <p>Selected: {{selected}}</p>
        </div>

        <button @click.alt="clickHandler('do something here')">
            Alt + Click
        </button>

        <!-- Reaction Timer -->
        <ReactionTimer />


        <!-- Multi Step Form -->
        <MultiStepForm :showMultiStep="showMultiStepForm" @close="showMultiStepForm = false" />

        <!-- Slots -->
        <SlotsCompo>
            <h1>That's Slot</h1>
        </SlotsCompo>

        <div class="todo-list">
            <form @submit.prevent="addNewTodo">
                <label for="new-todo">Add a todo</label>
                <input type="text" v-model="newTodoText" id="new-todo">
                <button>Add</button>
            </form>

            <ul v-if="todosItem">
                <TodosList v-for="(item, index) in todosItem" 
                :key="item.id" 
                :todo="item" 
                v-on:remove="todosItem.splice(index, 1)" />
            </ul>
        </div>
    </div>
</template>

<script>
import MultiStepForm from '@/components/MultiStepForm.vue';
import ReactionTimer from '@/components/ReactionTimer.vue';
import SlotsCompo from '@/components/SlotsCompo.vue';
import TodosList from '@/components/TodosList.vue';

export default {
    components: {
        MultiStepForm,
        ReactionTimer,
        SlotsCompo,
        TodosList
    },
    data() {
        return {
            quantityNum: 0,
            showMultiStepForm: false,
            loginPass: '',
            isLogin: true,
            isWrongPass: false,
            selected: 'a',
            isMultiselect: false,
            newTodoText: '',
            newTodoID: 2,
            todosItem: [
                {
                    id: 1,
                    title: 'Fruit'
                }
            ]
        }
    },
    methods: {
        incrementBtn: function() {
            this.quantityNum++;
        },
        decrementBtn: function() {
            if(this.quantityNum == 0) {
                this.quantityNum = 0;
            } else {
            this.quantityNum--;
            }
        },
        showMultiStep: function() {
            this.showMultiStepForm = true;
        },
        clickHandler: function($msg) {
            alert($msg);
        },
        enteredPass: function() {
            if( this.loginPass == '123') {
                this.isLogin = false;
                this.loginPass = '';
            } else {
                this.isWrongPass = true
                setTimeout(() => {
                    this.isWrongPass = false
                }, 3000);
            }
        },
        Multiselect: function() {
            this.isMultiselect = !this.isMultiselect
        },
        addNewTodo: function() {
            this.todosItem.push({
                id: this.newTodoID++,
                title: this.newTodoText,
            });
            this.newTodoText = ''
        }
    }
}
</script>

<style scoped>
    .events-wrapper {
        text-align: left;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        position: relative;
    }
    .events-wrapper > * {
        margin-bottom: 20px;
    }
    .quantity-box {
        display: inline-flex;
        align-items: center;
        height: 30px;
        border: 1px solid #ddd;
        overflow: hidden;
        border-radius: 30px;
    }
    .quantity-box button:first-child {
        font-size: 22px;
    }
    .quantity-box button {
        cursor: pointer;
        background: #eee;
        border: none;
        font-weight: 400;
        height: 30px;
        width: 30px;
        font-size: 14px;
        font-family: 'Roboto';
        padding: 0;
    }
    .quantity-box button:active {
        background: #f5f5f5;
    }
    .quantity-box .quantity-number {
        display: inline-block;
        width: 35px;
        text-align: center;
        font-weight: 400;
        height: 30px;
        line-height: 30px;
    }

    .show-multistep-form {
        background: #42b983;
        color: #fff;
        border: none;
        font-size: 14px;
        font-weight: 600;
        padding: 10px 20px;
        border-radius: 4px;
        margin: 0 15px 20px 0;
        cursor: pointer;
        box-shadow: 3px 3px 0 0 #2ea26e;
        transition: .2s;
    }
    .show-multistep-form:hover {
        box-shadow: 0px 0px 0 0 transparent;
    }
    .login {
        position: absolute;
        padding-top: 50px;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background: #fff;
        flex-direction: column;
        transition: all .5s;
        opacity: 1;
        visibility: visible;
    }
    .login input {
        border: 1px solid #ddd;
        padding: 5px 10px;
        border-radius: 4px;
    }
    .login button {
        border: none;
        height: 27px;
        margin-left: 5px;
        border-radius: 4px;
        padding: 5px 15px;
        cursor: pointer;
    }
    .login input:focus {
        outline: none;
        box-shadow: none;
    }
    .wrong-pass {
        color: red;
        margin: 10px 0 0 0;
        font-weight: 500;
        font-size: 14px;
    }
    .hide-login.login {
        opacity: 0;
        visibility: hidden;
    }
    .todo-list {
        width: 100%;
        max-width: 300px;
    }
    .todo-list form {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        margin-bottom: 10px;
    }
    .todo-list form input {
        flex: 1;
    }
    .todo-list form label {
        width: 100%;
        font-weight: 600;
    }
    .todo-list ul {
        margin: 0;
        padding: 0;
    }
    .todo-list ul li {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 8px;
        background: #f1f1f1;
        padding: 5px 10px;
        font-weight: 600;
        font-size: 13px;
        letter-spacing: 0.4px;
    }
    .todo-list ul li:last-child {
        margin-bottom: 0;
    }
</style>