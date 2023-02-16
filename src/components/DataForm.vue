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
     <div>
    <h3>Här kan jag lägga till och ändra företagen i listan</h3>
    <p>Vad vill jag göra?</p>
  </div>
    <form id="action">
        <label>Lägg till?</label>
        <input type="radio" v-model="check" value="POST">
        <label>Ändra?</label>
        <input type="radio" v-model="check" value="PUT">
        <label>Ta bort?</label>
        <input type="radio" v-model="check" value="DELETE">
    </form>
    <form v-if="check === 'POST'" class="post-form">
        <label>Företagets namn</label>
        <input type="text" v-model="formData.name">
        <label>Vilken typ av företag</label>
        <input type="text" v-model="formData.info">
        <label>Företagets plats</label>
        <input type="text" v-model="formData.location">
        <label>Inväntar svar</label>
        <input type="radio" v-model="formData.status" value="Inväntar svar">
        <label>Tackat nej</label>
        <input type="radio" v-model="formData.status" value="Tackat nej">
        <label>Kallad på intervju</label>
        <input type="radio" v-model="formData.status" value="Kallad på intervju">

        <input :disabled="formData.namn || formData.status == null" type="button" value="Lägg till" @click="formFunc('POST')" >

    </form>

    <form class="put-form" v-else-if="check === 'PUT'">
        <ul v-for="company in getCompanies">
            <li>{{ company.id }} {{ company.name }}</li>
        </ul>
        <label>Vilket ID vill jag ändra på</label>
        <input type="text" v-model="formData.putId">
        <label>Företagets namn</label>
        <input type="text" v-model="formData.name">
        <label>Vilken typ av företag</label>
        <input type="text" v-model="formData.info">
        <label>Företagets plats</label>
        <input type="text" v-model="formData.location">
        <label>Inväntar svar</label>
        <input type="radio" v-model="formData.status" value="Inväntar svar">
        <label>Tackat nej</label>
        <input type="radio" v-model="formData.status" value="Tackat nej">
        <label>Kallad på intervju</label>
        <input type="radio" v-model="formData.status" value="Kallad på intervju">

        <input type="submit" @click="formFunc('PUT')" value="Ändra">


    </form>


    <form v-else-if="check === 'DELETE'" class="delete-form">
        <ul v-for="company in getCompanies">
            <li>{{ company.id }} {{ company.name }}</li>
        </ul>
        <label>Företagets ID</label>
        <input type="text" v-model="formData.putId">

        <input v-if="showWarn === false" type="button" value="Ta bort" @click="showWarn = true">
    </form>
    <div v-if="showWarn"><p>Är du säker att du vill radera?</p>


    <input  type="button" value="Avbryt" @click="showWarn = false">
    <input type="button" value="Radera" @click="formFunc('DELETE')">
</div>


</section>
</template>

<style scoped>

.form {
    height: 90vh;
}

</style>
