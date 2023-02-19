<script>
    export default {
        props: {count: Number
    },

    }
</script>

<template>
    <section class="welcome">
        <div class="welcome-text">
          <h1>Välkommen till LIA-listan</h1>
          <h2>Där jag samlar all information om företag och   hur det går i processen att söka LIA
           </h2>
           <h2 v-if="count !== null">Just nu är det {{ count }} företag i listan.</h2>
        </div>
        <div class="welcome-space">

        </div>
    </section>
    <section class="list">

    </section>

</template>

<style scoped>

.welcome{
    background-image: url(../img/pexels-dominika-roseclay-1036808.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    min-height: 90vh;
    display: flex;
    align-items: center;
    flex-direction: row-reverse
;

}
.welcome-text {
    font-family: Roboto;
}
.welcome-text > h1 {
    font-size: 5rem;
    margin-bottom: 5vh;
}
.welcome-text > h2 {
    font-style: italic;
    font-size: 1.2rem;
    margin-top: 10vh;
}

.welcome-space {
    min-width: 50vw;

}
</style>
