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
        <h3>Inväntar svar</h3>
        <div class="list" id="list-1">
            <!-- <h3>Inväntar svar</h3> -->
            <ul v-for="company in companies">
                <li v-if="company.status === 'Inväntar svar'">
                    <p>{{ company.name }}</p>
                    <p>{{ company.info }}</p>
                    <p>{{ company.location }}</p>
                </li>
            </ul>
        </div>
        <h3>Tackat nej</h3>
        <div class="list" id="list-2">
            <!-- <h3>Tackat nej</h3> -->
            <ul v-for="company in companies">
                <li v-if="company.status === 'Tackat nej'"><p>{{ company.name }}</p>
                    <p>{{ company.info }}</p>
                    <p>{{ company.location }}</p>
                </li>
            </ul>
        </div>
        <h3>Kallad på intervju</h3>
        <div class="list" id="list-3">
            <!-- <h3>Kallad på intervju</h3> -->
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
        flex-direction: column;
        margin-top: 4vh;

    }

    ul{
        list-style-type: none;

    }

    li {
        width: 100vw;
        display: flex;
        justify-content: space-evenly;



    }


    li > p {
        font-size: 1rem;
        margin-top: 3vh;

    }
    h3{
        margin-top: 4vh;
        margin-left: 5vw;
    }

    .list {

        border-radius: 5px;
        display: flex;
        flex-direction: column;
        margin-left: 10vw

    }

     #list-1{
        background-color: rgba(255,255,0, 0.2);

    }




    #list-2{
        background-color: rgba(239, 90, 90, 0.1);
    }
    #list-3{
        background-color: rgba(66, 218, 96, 0.1);

    }

    p:nth-child(1) {
        font-weight: 600;
    }

    #btn {
       display: flex;
       justify-content: center;
       align-items: center;
       margin-top: 3vh;
    }

    button {
        text-decoration: none;
        border-radius: 15px;
        background-color: white;
        padding: 15px;
        font-size: 1rem;
        border: 1px solid black;
    }

    button:hover{
        padding: 15px 10px;
    }
</style>
