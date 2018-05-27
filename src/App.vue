<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <button class="btn btn-primary" @click="show = !show">Show Alert</button>
                <br><br>
                <transition name="fade">
                    <div class="alert alert-info" v-if="show">This is just an alert.</div>
                </transition>
                <transition name="slide" type="animation">
                    <div class="alert alert-info" v-if="show">This is just an alert.</div>
                </transition>
                <transition name="slide" type="animation" appear>
                    <div class="alert alert-info" v-show="show">This is just an alert.</div>
                </transition>
                <transition enter-active-class="animated bounce" leave-active-class="animated shake" appear>
                    <div class="alert alert-info" v-show="show">This is just an alert.</div>
                </transition>
                <hr>
                <transition name="fade" mode="out-in">
                    <div class="alert alert-info" v-if="show" key="info">This is just an alert.</div>
                    <div class="alert alert-warning" v-else key="warning">This is just a warning.</div>
                </transition>
                <hr>
                <h3>Transition using JS</h3>
                <button class="btn button-primary" @click="load = !load">Add/Remove Elements</button>
                <br>
                <br>
                <transition>
                    <div style="height: 100px; width: 100px; background-color: lightgreen;" v-if="load"></div>
                </transition>
                <hr>
                <h3>Transition between Components</h3>
                <button class="btn btn-primary" 
                @click="selectedComponent == 'app-success-alert' ? selectedComponent = 'app-danger-alert' : selectedComponent = 'app-success-alert'">Change Component</button>
                <br>
                <br>
                <transition name="fade" mode="out-in">
                    <component :is="selectedComponent"></component>
                </transition>
                <hr>
                <h3>Working with Transition Groups</h3>
                <input type="text" class="form-control" v-model="newItem" placeholder="Enter Item to be Added">
                <br>
                <button class="btn btn-primary" @click="addItem">Add Item</button>
                <br><br>
                <ul class="list-group">
                    <transition-group name="slide" tag="div">
                        <li class="list-group-item" v-for="(name, index) in names"  :key="name"> {{ name }} 
                        <small style="cursor: pointer; float: right; background-color: red; color: white; padding: 4px; border-radius: 4px;" @click="removeItem(index)">Remove</small>
                        </li>
                    </transition-group>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import DangerAlert from './dangerAlert.vue';
import SuccessAlert from './successAlert.vue';

    export default {
        data() {
            return {
                show: false,
                load: true,
                selectedComponent: 'app-success-alert',
                names: ['Ade', 'Tokunbo', 'Philip', 'Sandra'],
                newItem: ''
            }
        },
        components: {
            appDangerAlert: DangerAlert,
            appSuccessAlert: SuccessAlert
        },
        methods: {
            addItem() {
                this.names.push(this.newItem);
                this.newItem = '';
            },
            removeItem(index) {
                this.names.splice(index, 1);
            }
        }
    }
</script>

<style>
    .fade-enter {
        opacity: 0;
    }
    .fade-enter-active {
        transition: opacity 1s;
    }
    .fade-leave-active {
        transition: opacity 1s;
        opacity: 0;
    }
    .slide-enter {
        opacity: 0;
    }
    .slide-enter-active {
     animation: slide-in 1s ease-out forwards;   
     transition: opacity .5s;
    }  
    .slide-leave-active {
        animation: slide-out 1s ease-out forwards;
        transition: opacity 1s;
        opacity: 0;
        position: absolute;
    }
    .slide-move {
        transition: transform 1s;
    }
    @keyframes slide-in {
        from {
            transform: translateY(20px);
        }
        to {
            transform: translateY(0);
        }
    }
    @keyframes slide-out {
        from {
            transform: translateY(0);
        }
        to {
            transform: translateY(20px);
        }
    }
</style>
