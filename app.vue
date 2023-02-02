<!--<script>
export default {
props: ['username']
}
</script>-->

<template>
    <main>
      <h1>Zoznam ľudí</h1>
      <button class="delete" v-if="bool != true" v-on:click="DeleteButton">Delete</button>
      <section class="list">
          <section v-for="person of persons" v-bind:key="person" class="card-container">
        <personalCard @editWasClicked="click" @submitWasClicked="editPerson" @removeWasClicked="removePerson" v-bind:person="person"></personalCard>
      </section>
      </section>
      <input v-model="name" placeholder="Name" v-show="editBool != false">
      <div>{{name}}</div>
	  <!--<div id='account-info'>{{username}}</div>-->
    </main>
</template>



<script setup>

let initialPersons = [
        {
            fname: "Magdalena",
            lname: "Mikulova",
            birthday: 2000,
        },
        {
            fname: "Mirka",
            lname: "Makovicova",
            birthday: 1900,
        },
        {
            fname: "Hugo",
            lname: "Hugovic",
            birthday: 2017,
        },
        {
            fname: "Miki",
            lname: "Hric",
            birthday: 2003,
        },
        {
            fname: "Andrea",
            lname: "Veresova",
            birthday: 1982,
        },
        {
            fname: "Nora",
            lname: "Mojsejova",
            birthday: 2011,
        },
    ]

let persons = ref(initialPersons);

    let bool = ref(false);

    const DeleteButton = () => {
        bool.value = true;
        persons.value = [];
        name.value = ""
    }

//moze sa zapisat aj takto, bez state -> je ale lepsie zapisovat aj state, v reacte to bez state nebude fungovat
    /*let bool = false;
    const DeleteButton = () => {
        bool = true;
        persons.value = [];
    }*/

const removePerson = (personShouldBeRemoved) =>{
    persons.value = persons.value.filter(item=>item!=personShouldBeRemoved)
    }

let name = ref("")

let editBool = ref(false)

function click() {
   editBool.value = true;
}

const editPerson = (personShouldBeEdited) => {
	editBool.value = false;
    persons.value.forEach(item => {
        if(item==personShouldBeEdited){
            item.fname=name.value
        }
    }
    )
	name.value = ""
}

</script>



<style>
    @import url('https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;500;600;700&display=swap');
    body {
        font-size: 15px;    
        font-family: 'Oswald', sans-serif;
        padding: 1rem;
        background: linear-gradient(-45deg, #ee7752, #f628ef, #9581f4, #23a6d5, #23d5ab);
        background-size: 400% 400%;
        animation: gradient 10s ease infinite;
    }
    @keyframes gradient{
        0%{
            background-position: 0% 50%;
        }
        50%{
            background-position: 100% 50%;
        }
        100%{
            background-position: 0% 50%;
        }
    }
    main {
        display: flex;
        flex-direction: column;
        gap: .75rem;
    }
    .list {
        /*min-width: 25% of body;*/
        display: flex;
        gap: 20px;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: stretch;
        font-size: 1.2rem;
    }
    .card-container {
        flex-grow: 1;
    }
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
    .delete{
        padding: .75rem 2rem;
        color: rgb(255, 0, 0);
        background-color: black;
        width: 250px;
        flex-grow: 1;
        text-align: center;
        transition: .5s;
        font-size: 30px;
    }
</style>