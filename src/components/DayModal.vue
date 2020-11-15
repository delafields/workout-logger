<template>
    <div id="day-modal-2">
        <div id="day-wrapper">
            <h3 id="date">{{this.data.date}}</h3>
            <h3 class="workout-category">LIFT</h3>
            <p class="description">{{this.data.liftDescription}}</p>
            <h3 class="workout-category">CARDIO</h3>
            <p class="description" style="padding-bottom:20px;">{{this.data.cardioDescription}}</p>
        </div>
        <button id="close-button" @click="$emit('close')">CLOSE</button>
    </div>
</template>

<script>
  export default {
      name: 'DayModal',
    props: ['name', 'data']
  };
</script>

<style>
#day-wrapper {
    border-bottom: 4px solid #42CC8C;;
}

#day-data {
    color: white;
    text-decoration: underline;
}

/* Desktop/Tablet */
@media (min-width: 500px) {
    #date {
        color: white;
        font-family: 'Chivo', sans-serif;
        text-align: center;
        padding-top: 10px;
        font-size: 25px;
    }

    .workout-category {
        color: white;
        font-family: 'Chivo', sans-serif;
        letter-spacing: 2px;
        padding-left: 30px;
        padding-right: 30px;
    }

    .description {
        color: white;
        font-family: 'Roboto', sans-serif;
        font-weight: bold;
        padding-left: 30px;
        padding-right: 30px;
    }

    #close-button {
        width: 100%;
        height: 40px;
        background: rgb(15,32,39);
        background: linear-gradient(152deg, rgba(15,32,39,1) 0%, rgba(32,58,67,1) 21%, rgba(15,32,39,1) 100%);
        border: none;
        color: white;
        font-family: 'Chivo', sans-serif;
        font-size: 25px;
        cursor:pointer;
    }
}

/* Mobile */
@media (max-width: 499px) {
    #date {
        color: white;
        font-family: 'Chivo', sans-serif;
        text-align: center;
        padding-top: 10px;
        font-size: 16px;
    }

    .workout-category {
        color: white;
        font-family: 'Chivo', sans-serif;
        letter-spacing: 2px;
        padding-left: 30px;
        padding-right: 30px;
    }

    .description {
        color: white;
        font-family: 'Roboto', sans-serif;
        font-size: 12px;
        font-weight: bold;
        padding-left: 30px;
        padding-right: 30px;
    }

    #close-button {
        width: 100%;
        height: 40px;
        background: rgb(15,32,39);
        background: linear-gradient(152deg, rgba(15,32,39,1) 0%, rgba(32,58,67,1) 21%, rgba(15,32,39,1) 100%);
        border: none;
        color: white;
        font-family: 'Chivo', sans-serif;
        font-size: 16px;
        cursor:pointer;
    }
}

</style>