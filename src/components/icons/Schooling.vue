<script setup>
    import Page404 from './Page404.vue';

    const parcours = {
        annee1: {
            ecole: 'Université Lille 2',
            date: '2005',
            title: 'Licence éducation motricité',
            comment: 'Diplôme pour péparer au concours de professeur d'Eps'
        },
        annee2: {
            ecole: 'Lycée Yser Reims',
            date: '2000',
            title: 'BTS Topographique',
            comment: 'Diplôme pour devenir aide géomètre'
        },
        annee3: {
            ecole: 'Lycée Saint Adrien Villeneuve d'ascq',
            date: '1998',
            title: 'Baccalauréat',
            comment: 'Diplôme de fin d'étude de cycle classique'
        },
        }
    }
</script>

<template>
    <div class="courses">
        <div class="courses__title">
            <span class="material-symbols-outlined">history_edu</span><br>
            <TitreNiveau2>Mon parcours</TitreNiveau2>
        </div>
    
        <div class="parcours">
            <div class="ecole" v-for="annee in parcours">
                <h3 class="ecole__title">{{ annee.ecole }}</h3>
                <h4 class="ecole__info">{{ annee.title }} <span class="separation">|</span> {{ annee.date }}</h4>
                <p class="ecole__comment">{{ annee.comment }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .courses {
        width: 60%;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: auto;
    }

    .courses__title {
        text-align: center;
    }

    .material-symbols-outlined {
        font-size: 4em;
    }

    .ecole__title {
        font-size: 1.25em;
    }

    .ecole__info {
        font-size: 1.05em;
    }

    .separation {
        font-style: italic;
        color: #EFA48B;
    }

    .ecole__comment {
        text-indent: 2em;
        text-align: justify;
    }

    .parcours {
        margin-top: 15px;
        display: flex;
        flex-direction: column-reverse;
        gap: 25px;
    }

    .ecole {
        padding: 15px;
        background-color: #EFFAFD;
        border-radius: 25px;
        box-shadow: -4px 5px 10px #B0B347;
    }

    @media screen and (max-width: 480px) {
        .courses {
            width: 85%;
        }
    }
</style>