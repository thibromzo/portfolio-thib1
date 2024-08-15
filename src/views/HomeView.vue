<script setup>
    import { ref, computed } from 'vue';
    import creationModal from '../components/creationModal.vue';
    import CreationArticle from '../components/CreationArticle.vue';
     
    import modalAllConfig from '../assets/content/modalAllConfig'
    import creationArticleContent from '../assets/content/creationArticleContent';

    const articleContent = ref(creationArticleContent);

    const modalConfig = ref({
        display: "none",
        content: {
            title: "",
            creationDate: "",
            fileLink: "",
            gitLink: ""}
    });

    const messageContent = ref({
        firsname:"",
        lastname:"",
        object:"",
        message:"",
    });

    //Construct mail request with form user entries
    const emailMe = computed(()=>{
        const mailBody = encodeURIComponent(
            "Nom: " + messageContent.value.firsname + "\nPrénom: " + messageContent.value.lastname + "\nMessage:" + "\n" + messageContent.value.message);

        return `mailto:${import.meta.env.VITE_MAIL}?subject=${messageContent.value.object}&body=${mailBody}`;
    });

    //HTML element ID: underline property
    const isUnderline = ref({
        prez: "none",
        creation: "none",
        contact: "none"
    });

    //Similar of a CSS :hover but for any HTML element target ID in isUnderline
    function changeUnderline(event) {
        const newState = isUnderline.value[event.target.id] == "none" ? "underline" : "none";
        isUnderline.value[event.target.id] = newState;
    };

    function onModalClickClose() {
        modalConfig.value.display = 'none';
    };

    function onCreationClick(creationName) {
        modalConfig.value = modalAllConfig[creationName];
        modalConfig.value.display = 'block';
    };
</script>

<template>
    <header class="col-flex-wrap-center">
        <figure class="photo-profile">
        <a href="/#main">
            <img class="photo-profile__img"
                src="/pictures/photo_profile_thib.jpg"
                title="Photo profile Thibaud Liagre"
                alt="La photo de Thibaud Liagre">
        </a>
        </figure>
        <nav class="row-flex-wrap-center">
            <a id="prez_link" href="#prez" :style="{ textDecoration: isUnderline.prez }" class="menu-item-link">Présentation</a>
            <a id="creation_link" href="#creation" :style="{ textDecoration: isUnderline.creation }" class="menu-item-link">Création</a>
            <a id="contact_link" href="#contact" :style="{ textDecoration: isUnderline.contact }" class="menu-item-link">Contact</a>
        </nav>
    </header>
    <main id="main">
        <creationModal @close-clicked="onModalClickClose" :modal-config=modalConfig />
        <section id="prez" @mouseenter="changeUnderline" @mouseleave="changeUnderline" class="text-center col-flex-wrap-center">
            <h1 class="presentation-titre">Thibaud Liagre</h1>
            <p class="presentation-text">
                Je suis actuellement en formation de "Développeur Web et Mobile" avec le "Centre Européen de Formation", 
                Dans ce portfolio vous allez découvrir quelques unes de mes réalisations.
            </p>
        </section>
        <section id="creation" @mouseenter="changeUnderline" @mouseleave="changeUnderline" class="text-center col-flex-wrap-center">
            <h2>Mes créations</h2>
            <div class="row-flex-wrap-center space-around">
                <CreationArticle v-for="article in articleContent" 
                    :key="article.name" 
                    :article-content="article"
                    @creation-clicked="onCreationClick" />
            </div>
        </section>
        <section id="contact" @mouseenter="changeUnderline" @mouseleave="changeUnderline" class="text-center col-flex-wrap-center">
            <h2>Contact</h2>
            <form :action="emailMe" method="post" enctype="application/x-www-form-urlencoded">
                <div class="row-flew-wrap-center">
                    <label>Nom :
                        <input required type="text" v-model="messageContent.firsname" id="firstname" placeholder="Votre nom...">
                    </label>
                    <label>Prénom :
                        <input required type="text" v-model="messageContent.lastname" id="lastname" placeholder="Votre prénom...">
                    </label>
                </div>  
                <label>Objet :
                    <input required type="text" v-model="messageContent.object" id="object" placeholder="objet du message">
                </label>
                <textarea required v-model="messageContent.message" id="message" placeholder="Votre message"></textarea>
                <button type="submit">Envoyer</button> 
            </form>
        </section>
    </main>
    <footer class="col-flex-wrap-center">
        <div class="row-flex-wrap-center footer__icons">
            <figure class="footer__icon">
                <a href="https://www.linkedin.com/in/thibaud-liagre-aa0534177" target="_blank">
                <img src="/icons/linkedin.png"
                    title="Vers mon linkedin"
                    alt="Lien vers le linkedin de Thibaud Liagre">
                </a>
            </figure>
            <figure class="footer__icon">
                <a href="https://github.com/thibromzo/" target="_blank">
                <img src="/icons/github.png"
                    title="Vers mon github"
                    alt="Lien vers le GitHub de Thibaud Liagre">
                </a>
            </figure>
        </div>
        <p><small>Dernière mise à jour le <time datetime="2024-07-26">26/07/2024</time></small></p>
    </footer>
</template>

<style scoped>
    nav {
            width: 50%;
            justify-content: space-around;
    }

    nav > a:hover {
        color: cadetblue;
    }

    section {
        border-top: 1px solid black;
    }

    form {
        display: flex;
        flex-direction: column;
        width: fit-content;
        border: 2px solid black;
        border-radius: 10px;
    }

    input {
        height: 1.5rem;
        width: 150px;
        margin-top: 10px;
        margin-right: 10px;
        margin-bottom: 10px;
        border: 1px solid black;
        border-radius: 5px;
    }

    label {
        margin-left: 10px;
        font-weight: bold;
    }

    textarea {
        height: 100px;
        margin-left: 10px;
        margin-right: 10px;
    }
    .menu-item-link {
        text-decoration: none;
        font-size: 1.5rem;
    }
    .photo-profile {
        width: 150px;
        height: 150px;
        margin-top: 30px;
    }

    button {
        margin-top: 10px;
        margin-bottom: 10px;
        margin-left: auto;
        margin-right: auto;
        width: fit-content;
    }

    .photo-profile__img {
        border-radius: 50%;
        box-shadow: 0 0 15px black;
    }

    .space-around {
        width: 90%;
        justify-content: space-between;
    }
    .presentation-titre {
        margin: 1rem;
        font-size: 3rem;
    }

    .presentation-text {
        width: 60%;
        margin-top: 0px;
    }
    .footer__icons {
      margin-top: 10px;
   }

    .footer__icon {
        width: 50px;
        height: 50px;
        margin: 10px;
    }

    .footer__icon img:hover {
        opacity: 0.5;
    }
</style>