<script>
    export default {
        emits: ['changedCount'],
        created() {
            this.fetch();
        },

        data() {
            return {
                listClass: "list-class",
                companies: null,

            };
        },

        methods: {
            fetch(){

                 // fetch('/info.json')
                fetch('http://localhost:3000/companies')
                .then((response) => response.json())
                .then((result) =>  {
                    this.companies = result;
                    })

            },

             companyCount(){
                 this.$emit('changedCount', this.companies.length)
            }
        },

    }
</script>

<template>
    <section :class="listClass">

        <div class="list" id="list-1">
            <h3>Inväntar svar</h3>
            <ul v-for="company in companies">
                <li v-if="company.status === 'Inväntar svar'">
                    <p>{{ company.name }}</p>
                    <p>{{ company.info }}</p>
                    <p>{{ company.location }}</p>
                </li>
            </ul>
        </div>
        <div class="list" id="list-2">
            <h3>Tackat nej</h3>
            <ul v-for="company in companies">
                <li v-if="company.status === 'Tackat nej'"><p>{{ company.name }}</p>
                    <p>{{ company.info }}</p>
                    <p>{{ company.location }}</p>
                </li>
            </ul>
        </div>
        <div class="list" id="list-3">
            <h3>Kallad på intervju</h3>
            <ul v-for="company in companies">
                <li v-if="company.status === 'Kallad på intervju'"><p>{{ company.name }}</p>
                    <p>{{ company.info }}</p>
                    <p>{{ company.location }}</p></li>
            </ul>
        </div>
    </section>
    <div id="btn">
        <button @click="fetch(), companyCount()">Uppdatera listan</button>
    </div>
    <!-- <input type="button" @click="companyCount()" value="iaisdaisd"> -->
</template>

<style scoped>
    .list-class {
        font-family: Roboto;
        display: flex;
        justify-content: space-evenly;
        align-items: flex-start;

        margin-top: 5vh;

    }

    ul{
        list-style-type: none;

    }

    li {
        margin: 7vh;
        border: 1px solid black;
        border-radius: 20px;
        width: 200px;
        height: 150px;


    }

    li > p {
        font-size: 1.3rem;
        margin-top: 1.5vh;
    }
    h3{
        margin-top: 4vh;
    }

    .list {
        min-width: 300px;
        text-align: center;
        border-radius: 20px;

    }

    #list-1{
        background-color: rgba(255,255,0, 0.2);

    }
    #list-2{
        background-color: rgba(239, 90, 90, 0.1);
    }
    #list-3{
        background-color: rgba(118, 211, 136, 0.1);
    }

    #btn {
       display: flex;
       justify-content: center;
       align-items: center;
    }

    button {
        text-decoration: none;
        border-radius: 30px;
        background-color: white;
        padding: 10px;
        font-size: 1.2rem;
    }

    button:hover{
        padding: 10px 15px;
    }
</style>
