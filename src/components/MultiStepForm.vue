<template>
    <div v-if="showMultiStep" class="multistep-form-sidebar">
        <span @click="closeMultistep" class="close-multistep-form-sidebar">+</span>

        <div class="multistep-lists">
            <div :class="stepNumber === 1 ? 'active-form multistep-form-step1' : 'multistep-form-step1'">
                <h1>Step 1</h1>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Architecto, pariatur eius consequuntur recusandae tempora provident consequatur. Neque officiis rem suscipit.</p>
                <form>
                    <div class="input-group">
                        <label for="">Name</label>
                        <input type="text" placeholder="Name" v-model="name">
                    </div>
                    <div class="input-group">
                        <label for="">Email</label>
                        <input type="email" placeholder="Email" v-model="email">
                    </div>
                    <div class="input-group">
                        <label for="">Message</label>
                        <textarea name="message" id="message" placeholder="Message" v-model="message"></textarea>
                    </div>
                </form>
                <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>
            </div>

            <div :class="stepNumber === 2 ? 'active-form multistep-form-step2' : 'multistep-form-step2'">
                <h1>Step 2</h1>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Architecto, pariatur eius consequuntur recusandae tempora provident consequatur. Neque officiis rem suscipit.</p>
                <ul>
                    <li>Lorem ipsum dolor sit amet.</li>
                    <li>Lorem ipsum dolor sit amet.</li>
                    <li>Lorem ipsum dolor sit amet.</li>
                    <li>Lorem ipsum dolor sit amet.</li>
                </ul>
            </div>

            <div :class="stepNumber === 3 ? 'active-form multistep-form-step3' : 'multistep-form-step3'">
                <h1>Step 3</h1>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Architecto, pariatur eius consequuntur recusandae tempora provident consequatur. Neque officiis rem suscipit.</p>
                <div class="step1-form-content">
                    <div v-if="name" class="content-box">
                        <h3>Name</h3>
                        <p>{{name}}</p>
                    </div>
                    <div v-if="email" class="content-box">
                        <h3>Email</h3>
                        <p>{{email}}</p>
                    </div>
                    <div v-if="message" class="content-box">
                        <h3>Message</h3>
                        <p>{{message}}</p>
                    </div>
                </div>
                <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>
            </div>

            <div :class="stepNumber === 4 ? 'active-form multistep-form-step4' : 'multistep-form-step4'">
                <h1>Thank You MultiStep</h1>
            </div>
        </div>

        <div class="multistep-form-buttons">
            <button v-if="stepNumber === 2 || stepNumber === 3" class="multistep-form-back-btn" @click="backStep">
                Back
            </button>
            <button v-if="stepNumber === 1" class="disabled multistep-form-back-btn" disabled>
                Back
            </button>
            <button v-if="stepNumber === 1 || stepNumber === 2 || stepNumber === 3" @click="nextStep" class="multistep-form-next-btn">
                {{stepNumber == 1 || stepNumber == 2 ? 'Next' : 'Confirm'}}
            </button>
            <button v-if="stepNumber === 4" @click="closeMultistep" class="multistep-form-next-btn done">
                Close
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: ['showMultiStep'],
    data() {
        return {
            stepNumber: 1,
            name: '',
            email: '',
            message: ''
        }
    },
    methods: {
        nextStep: function() {
            // if (this.stepNumber == 5) {
                // alert('next lavel 5');
            // } else {
                this.stepNumber ++;
            // }
        },
        backStep: function() {
            if (this.stepNumber == 1) {
                this.stepNumber = 1;
            } else {
                this.stepNumber --;
            }
        },
        closeMultistep: function() {
            this.$emit('close');
            this.stepNumber = 1;
            this.name = '',
            this.email = '',
            this.message = ''
        }
    }
}
</script>

<style scoped>
    .multistep-form-sidebar {
        position: fixed;
        right: 0;
        top: 0;
        width: 350px;
        padding: 20px;
        height: 100%;
        overflow: hidden;
        border: 1px solid #eee;
        background: #fff;
        box-shadow: 0 0 30px rgb(0 0 0 / 10%);
    }
    .close-multistep-form-sidebar {
        position: absolute;
        right: -24px;
        top: -6px;
        width: 70px;
        height: 36px;
        font-size: 19px;
        text-align: center;
        line-height: 41px;
        background: #000;
        font-weight: 700;
        color: #fff;
        cursor: pointer;
        transform: rotate(45deg);
        z-index: 999;
    }
    .multistep-form-buttons {
        position: absolute;
        bottom: 0;
        width: 100%;
        left: 0;
        padding: 10px 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .multistep-form-sidebar h1 {
        font-weight: 700;
            text-transform: uppercase;
    }
    .multistep-form-sidebar p {
        font-size: 16px;
        margin: 0 0 15px 0;
        line-height: 1.5;
    }
    .multistep-form-sidebar form .input-group {
        margin-bottom: 15px;
    }
    .multistep-form-sidebar form .input-group label {
        display: block;
        font-size: 14px;
        font-weight: 700;
        margin: 0 0 5px 0;
    }
    .multistep-form-sidebar form .input-group textarea,
    .multistep-form-sidebar form .input-group input {
        width: 100%;
        border: 1px solid #eee;
        padding: 10px 15px;
        border-radius: 4px;
        font-size: 13px;
    }
    .multistep-form-buttons button {
        background: #42b983;
        color: #fff;
        border: none;
        font-size: 14px;
        font-weight: 600;
        padding: 8px 20px;
        border-radius: 4px;
        margin: 0 15px;
        cursor: pointer;
        box-shadow: 3px 3px 0 0 #2ea26e;
        transition: .2s;
        text-align: center;
        width: 49%;
    }
    .multistep-form-buttons button.done,
    .multistep-form-buttons .multistep-form-back-btn {
        background: #000;
        box-shadow: 3px 3px 0 0 #dcdcdc;
    }
    .multistep-form-buttons button.done {
        width: 100%;
    }
    .disabled {
        opacity: 0.2;
        cursor: no-drop !important;
    }
    .step1-form-content {
        border: 1px solid #eee;
        border-radius: 4px;
        margin-bottom: 10px;
    }
    .step1-form-content .content-box {
        border-bottom: 1px solid #eee;
        padding: 10px 20px;
    }
    .step1-form-content .content-box:last-child {
        border: none;
    }
    .step1-form-content .content-box h3 {
        font-size: 16px;
        font-weight: 700;
        margin: 0 0 6px 0;
    }
    .step1-form-content .content-box p {
        margin: 0;
        color: #777;
        font-size: 15px;
    }
    .multistep-lists > * {
        opacity: 0;
        visibility: hidden;
        position: absolute;
        left: 0;
        top: 0;
        transform-origin: top;
        transform: rotateY(90deg);
        transition: all .3s;
        background: #fff;
    }
    .multistep-lists {
        width: 100%;
        height: 94%;
        position: relative;
        overflow-x: hidden;
    }
    .multistep-lists .active-form {
        opacity: 1;
        visibility: visible;
        transform: rotateY(0);
        transition: all .5s;
    }
</style>