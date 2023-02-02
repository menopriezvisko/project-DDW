<script setup>
    defineProps(['person'])

const vek = function (person){
    let year = new Date().getFullYear()
    return  year - person.birthday;
    }

let editBool = ref(false)

function beingEdited() {
   editBool.value = true
}

function edited(){
    editBool.value = false
}

//let name = ref("")

//<account-info username='matt' />

</script>

<template>
    <section v-bind:class="person.age>=18 ? 'adult card-container card' : 'card-container card'">
        
          <article class="info">
			<!--<div v-if="editBool != false" class="name"><input v-model="name" placeholder="Name" v-show="editBool != false"> {{person.lname}}</div>
			<div v-else class="name">{{person.fname}} {{person.lname}}</div>-->
            <div class="name">{{person.fname}} {{person.lname}}</div>
            <div>{{vek(person)}}</div>
            <div class="birthday">{{person.birthday}} <span class="year-title">year of birth</span></div>
          </article>
          <footer class="footer-card">
			<span class="btn edit" v-on:click="beingEdited()" @click="$emit('editWasClicked')" v-if="editBool != true">Edit</span>
			<span class="btn remove" v-on:click="$emit('removeWasClicked', person)" v-show="editBool != true">Remove</span>
			<span class="btn submit" @click="$emit('submitWasClicked', person)" v-show="editBool != false" v-on:click="edited()">Submit</span>
          </footer>
        </section>
</template>


<style scoped>
    .card {
        background: rgba(255,255,255, 1);
        border: 1px solid #bbb;
        color: #444;
        box-shadow: 0 3px 5px rgba(0,0,0,.2);
        border-top-width: 5px;
        border-top-color: rgb(0, 128, 255);
    }
    .card.adult {
        border-top-color: rgb(255, 0, 0);
    }
    .card.old {
        border-top-color: rgb(0, 0, 0);
    }
    .card:hover {
        border: 5px solid;
        color: #444;
        box-shadow: 3px 4px 6px 9px rgba(0,0,0,.5);
    }
    .info {
        padding: 1rem;
        text-align: center;
        font-size: 1.3rem;
    }
    .name {
        font-size: 50px;
        font-weight: bold;

        }
    .age {
        font-weight: 1000;
        font-size: 40px;
    }
    .birthday{
        font-size: 25px;
        font-weight: bold;
    }
    .year-title {
        color: #00000081;
    }
    .footer-card {
        display: flex;
    }
    .btn {
        padding: .75rem 2rem;
        color: white;
        width: 50px;
        flex-grow: 1;
        text-align: center;
        transition: .5s;
        font-size: 30px;
    }
    .btn.edit {
        background: rgb(91, 236, 91);
    }
    .btn.remove {
        background: red;
    }
	.btn.submit {
	background: rgb(19, 19, 194);
}
    .btn:hover {
        opacity: .3;
        cursor: pointer;;
    }
    .list:hover .card-container{
        filter: blur(3px);
        opacity: .5;
        transform: scale(.98);
    }
    .list:hover .card-container:hover{
        transform: scale(1);
        filter: blur(0px);
        opacity: 1;
        box-shadow: 0 8px 20px 0 rgba(0, 0, 0, 0.25);
    }
</style>