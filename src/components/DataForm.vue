<script>
export default {
    created(){

                // fetch('/info.json')
                fetch('http://localhost:3000/companies')
                .then((response) => response.json())
                .then((result) =>  {
                    this.getCompanies = result;
                    });


},
    data(){
        return {
            check: null,
            formData: {
                id:null,
                name: null,
                info: null,
                location: null,
                status: null,
                putId: null
             },

            showWarn: false,

            getCompanies: null,

        }

    },
    methods: {
        formFunc(method){
            if(method === 'POST') {
        fetch('http://localhost:3000/companies', {
            method: method,
            headers: {
                'Accept': 'application/json, text/plain, */*',
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                id: this.getCompanies.length + 1,
                name: this.formData.name,
                info: this.formData.info,
                location: this.formData.location,
                status: this.formData.status
            }),
            })
            .then((response) => response.json())
            .then((result) => {
                this.getCompanies = result
                console.log('Success:', result);
                this.formData.id = null,
                this.formData. name = null,
                this.formData.info = null,
                this.formData.location = null,
                this.formData.status = null,
                created()
            })
        }
        else if (method === 'PUT') {
            fetch('http://localhost:3000/companies/' + this.formData.putId, {
            method: method,
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({

                name: this.formData.name,
                info: this.formData.info,
                location: this.formData.location,
                status: this.formData.status
            }),
            })
            .then((response) => response.json())
            .then((result) => {
                this.getCompanies = result
                console.log('Success:', result);
                created();
            })
        }
        else {
            fetch('http://localhost:3000/companies/' + this.formData.putId, {
            method: method
            })
            .then((response) => response.json())
            .then((result) => {
                this.getCompanies = result
                console.log('Success:', result);
                this.showWarn = false;
                this.formData.putId = null
                created();

            })
        }
    }
},
    watch: {
        check(checkWas, checkIs) {
            console.log(checkIs, checkWas )
        }
    }
}

</script>

<template>
    <section class="form">
     <div class="hero">
    <h3>H??r kan jag l??gga till och ??ndra f??retagen i listan</h3>
    <p>Vad vill jag g??ra?</p>
  </div>
    <form id="action">
        <label>L??gg till?</label>
        <input type="radio" v-model="check" value="POST">
        <label>??ndra?</label>
        <input type="radio" v-model="check" value="PUT">
        <label>Ta bort?</label>
        <input type="radio" v-model="check" value="DELETE">
    </form>
    <form v-if="check === 'POST'" class="post-form">
        <label>F??retagets namn</label>
        <input type="text" v-model="formData.name">
        <label>Vilken typ av f??retag</label>
        <input type="text" v-model="formData.info">
        <label>F??retagets plats</label>
        <input type="text" v-model="formData.location">
        <label>Inv??ntar svar</label>
        <input type="radio" v-model="formData.status" value="Inv??ntar svar">
        <label>Tackat nej</label>
        <input type="radio" v-model="formData.status" value="Tackat nej">
        <label>Kallad p?? intervju</label>
        <input type="radio" v-model="formData.status" value="Kallad p?? intervju">

        <input :disabled="formData.namn || formData.status == null" type="button" value="L??gg till" @click="formFunc('POST')" >

    </form>

    <form class="put-form" v-else-if="check === 'PUT'">
        <div class="put-comp-list">
            <ul v-for="company in getCompanies">
                <li>{{ company.id }} {{ company.name }}</li>
            </ul>
        </div>
        <div class="put-comp-form">
            <label>Vilket ID vill jag ??ndra p??</label>
            <input type="text" v-model="formData.putId">
            <label>F??retagets namn</label>
            <input type="text" v-model="formData.name">
            <label>Vilken typ av f??retag</label>
            <input type="text" v-model="formData.info">
            <label>F??retagets plats</label>
            <input type="text" v-model="formData.location">
            <label>Inv??ntar svar</label>
            <input type="radio" v-model="formData.status" value="Inv??ntar svar">
            <label>Tackat nej</label>
            <input type="radio" v-model="formData.status" value="Tackat nej">
            <label>Kallad p?? intervju</label>
            <input type="radio" v-model="formData.status" value="Kallad p?? intervju">

            <input type="submit" @click="formFunc('PUT')" value="??ndra">
        </div>

    </form>


    <form v-else-if="check === 'DELETE'" class="delete-form">
        <div class="delete-comp-list">
            <ul v-for="company in getCompanies">
                <li>{{ company.id }} {{ company.name }}</li>
            </ul>
        </div>
        <div class="delete-comp-form">
        <label>F??retagets ID</label>
        <input type="text" v-model="formData.putId">

        <input v-if="showWarn === false" type="button" :disabled="formData.putId === null" value="Ta bort" @click="showWarn = true">


    <div v-if="showWarn"><p>??r du s??ker att du vill radera?</p>


    <input  type="button" value="Avbryt" @click="showWarn = false">
    <input type="button" value="Radera" @click="formFunc('DELETE')">
    </div>
    </div>
</form>


</section>
</template>

<style scoped>

.form {
    height: 90vh;
    margin-left: 5vw;
}

.hero > p {
    font-weight: 700;
    margin-top: 10vh;
}


#action {
    display: flex;
    flex-direction: row;

}
#action > label {
    margin-left: 2vw;
    margin-right: 1vw;

}

li{
    list-style-type: none
    ;
}

.post-form {
    display: flex;
    flex-direction: column;
    align-items: start;
    width: 200px;
    margin: 4vh 0 0 55vw;
}
.put-form {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    margin-top: 4vh;
}

.put-comp-form {
    display: flex;
    flex-direction: column;
}

.delete-form {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    margin-top: 4vh;
}

.delete-comp-form{
    display: flex;
    flex-direction: column;

}
.delete-comp-form > input{
    margin-top: 3vh;

}


</style>
