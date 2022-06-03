<template>
    <div v-if="hearts" id="game-wrapper">
        <StatisticsComponent :hearts="hearts" :score="score" />
        <img v-if="dogImage" :src="dogImage" alt="dog" />
        <div v-else id="loading">Loading...</div>
        <div id="options">
            <button v-for="option in options" :key="option" @click="handleOption(option)">{{ option }}</button>
        </div>
    </div>
    <SummaryComponent v-else :score="score" @handlePlayAgain="handlePlayAgain" />
</template>
<script>
import StatisticsComponent from './StatisticsComponent.vue';
import SummaryComponent from './SummaryComponent.vue';

export default {
    name: 'GameComponent',
    components: {
        StatisticsComponent,
        SummaryComponent,
    },
    data() {
        return {
            dogImage: null,
            pickedBreed: null,
            options: null,
            score: 0,
            hearts: 3,
        }
    },
    methods: {
        async fetchData() {
            const BREEDS_API = 'https://dog.ceo/api/breeds/list/all';
            try {
                const res = await fetch(BREEDS_API);
                const data = await res.json();

                let breeds = Object.keys(data.message);

                let breedsAndSubbreads = [];

                breeds.forEach((breed) => {
                    let subbreads = data.message[breed];
                    if (!subbreads.length) {
                        breedsAndSubbreads.push(breed);
                    }

                    subbreads.forEach((subbread) => {
                        breedsAndSubbreads.push(breed + ' ' + subbread);
                    });
                });

                this.pickedBreed = breedsAndSubbreads.splice(Math.floor(Math.random() * breedsAndSubbreads.length), 1)[0];

                // shuffle breedsAndSubbreads array
                breedsAndSubbreads.sort(() => Math.random() - 0.5);

                this.options = breedsAndSubbreads.slice(0, 3);
                this.options.push(this.pickedBreed);
                // shuffle options array
                this.options.sort(() => Math.random() - 0.5);

            } catch (error) {
                console.log(error);
            }

            let RANDOM_BREED_API = '';

            if (this.pickedBreed.indexOf(' ') !== -1) {
                const [bread, subbread] = this.pickedBreed.split(' ');
                RANDOM_BREED_API = `https://dog.ceo/api/breed/${bread}/${subbread}/images/random`;
            } else {
                RANDOM_BREED_API = `https://dog.ceo/api/breed/${this.pickedBreed}/images/random`;
            }

            try {
                const res = await fetch(RANDOM_BREED_API);
                const data = await res.json();
                this.dogImage = data.message;
            } catch (error) {
                console.log(error);
            }
        },
        handleOption(option) {
            if (!this.hearts) return;
            if (option === this.pickedBreed) {
                this.fetchData();
                this.score++;
            } else {
                this.hearts--;
            }
        },
        handlePlayAgain() {
            this.hearts = 3;
            this.score = 0;
            this.fetchData();
        },
    },
    mounted() {
        this.fetchData();
    },
}
</script>
<style scoped>
#game-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

#loading {
    margin: 50px;
}

#options {
    width: 100%;
    margin-top: 2vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px;
}
</style>