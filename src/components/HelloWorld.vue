<template>
   <v-container id="projects" class="listingProject">
        <v-card class="my-4">
            <v-card-title>Filtre selon le type de projet qui t'intéresse !</v-card-title>
            <v-card-text>
              <v-chip class="bg-deepblue" v-for="(tech, index) in filters" :key="index" @click="toggleFilter(tech)">
                {{ tech }}
              </v-chip>
            </v-card-text>
          </v-card>
      <v-row>
        <v-col v-for="project in filteredProjects" :key="project.id" cols="12" md="4">
          <v-card class="my-4 pa-2">
            <v-img :src="project.imageSrc" height="200px"></v-img>
            <v-card-title class="my-1">{{ project.name }}</v-card-title>
            <v-card-text>{{ project.description }}</v-card-text>
            <v-card-subtitle class="mt-1">Technologies :</v-card-subtitle>
            <v-chip v-for="tech in project.technologies" :key="tech" class='bg-mediumblue'>{{ tech }}</v-chip>
            <v-btn width="100%" class="mt-3" color="deepblue" @click="showPopup(project)">
            Voir les détails
          </v-btn>

          <v-dialog v-model="popupVisible" width="500px">
            <v-card class="pa-2">
              <v-img :src="currentProject.imageSrc" height="200px"></v-img>
              <v-card-title class="my-3">{{ currentProject.name }}</v-card-title>
              <v-card-text>{{ currentProject.longDescription }}</v-card-text>
              <v-btn color="deepblue" class="mt-3" @click="popupVisible = false">
                Fermer
              </v-btn>
            </v-card>
          </v-dialog>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
<script>
  export default {
  data() {
    return {
      filters: ['Web', 'Jeux', 'DevOps', 'C#','Docker', 'Java','Javascript', 'Golang', 'Laravel', 'MongoDB', 'MySQL', 'PHP','React', 'Unity','Vue.js'],
      projects: [
        {
          id: 1,
          name: 'YDiscover',
          link : 'https://main.dmnepnuwu4hll.amplifyapp.com/',
          description: 'Création d\'un site de recommandations d\'artistes et génération de fond d\'écran.',
          imageSrc: 'src/assets/bg_card/project_1.PNG',
          longDescription:'Afin de perfectionner ma compréhension du PHP, de la POO et de MySQL, j’ai réalisé un site d’e-commerce en me basant sur le modèle MVC et en intégrant une API de paiement. Ce projet m’a permis notamment de mieux appréhender les fraweworks que sont Symfony et Laravel.',
          technologies: ['Web'],
        },
        {
          id: 2,
          name: 'YFleet',
          description: 'Création d\'une plateforme web de gestion de logistique et de transport',
          longDescription:'Notre plateforme basée sur des micro services vise à automatiser et optimiser les processus de transport pour les entreprises. Avec notre plateforme, vous pouvez y planifier les itinéraires de manière efficace pour maximiser la productivité, gérer facilement votre flotte en temps réel, suivre les marchandises en toute transparence et réduire la charge de travail des équipes de transport',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['React', 'Golang', 'MongoDB', 'Microservices', 'Docker','Développement web', 'DevOps'],
        },
        {
          id: 3,
          name: 'Forum',
          description: 'Création d\'un forum web reprenant les code des réseaux sociaux',
          longDescription:'Dernier projet de ma première année d’études, j’ai pu mettre en application l’intégralité des connaissances acquises en Golang en recréant un équivalent de Twitter en quelques semaines.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['HTML', 'Golang', 'CSS', 'Javascript', 'Github', 'Travail en équipe','Développement web'],
        },
        {
          id: 4,
          name: 'Hangman Web',
          description: 'Création d\'un forum web reprenant les code des réseaux sociaux',
          longDescription:"Sur le même principe que le projet console, il fallait recréer le jeu du pendu mais cette fois-ci sur un format exécutable par un navigateur.",
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['HTML', 'Golang', 'CSS', 'Javascript', 'Github', 'Travail en équipe','Développement web'],
        },
        {
          id: 5,
          name: 'Groupie Tracker',
          description: 'Création d\'un site de listing de musiques et `d\'artistes',
          longDescription:'Pour mieux comprendre l’utilisation des API, j’ai créé un site web référençant les données d’une API de musiques fournie en local. À cela se rajoute l’API Spotify et ses données ce qui rend le site encore à jour au moment où vous lisez ces lignes. Les musiques affichées peuvent être lues par le biais d’un lecteur intégré et être recherchées par le biais d’une barre de recherche.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['HTML', 'Golang', 'CSS', 'Javascript','Github', 'Travail en équipe','Développement web'],
        },
        {
          id: 5,
          name: 'YStock',
          description: 'Création d\'un logiciel de gestion de stock d\'une boutique en ligne',
          longDescription:'Dans la continuité du site d’e-commerce réalisé en PHP, il nous a été demandé de réaliser un logiciel permettant de gérer les stocks de ladite boutique en ligne.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['C#', 'WPF', 'MySQL', 'Interfaçage', 'Développement logiciel'],
        },
        {
          id: 6,
          name: 'YGame',
          description: 'Création d\'un jeu vidéo avec un système de leveling et de parcours de map',
          longDescription:'Afin de découvrir le game programming nous nous sommes initier à Unity et avons dû créer un jeu. J\'ai pu appréhender l\'utilisation des touches pour me déplacer et la gestion des niveaux.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['C#', 'Unity', 'Game Programming', 'Interfaçage', 'Game Design','Développement logiciel'],
        },
        {
          id: 7,
          name: 'Hangman',
          description: 'Création d\'un jeu du pendu avec gestion des différents statuts de partie',
          longDescription:'Premier projet de ma scolarité, il m’a permis de mettre en exergue les différentes compétences techniques acquises durant les 30 jours d’apprentissage intensif du langage Golang.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['Golang', 'Serveur', 'Développement logiciel', 'Interfaçage', 'Game Design'],
        },
        {
          id: 8,
          name: 'Moteur de recherche de films',
          description: 'Création d\'un système de moteur de recherche de films',
          longDescription:'Afin de consolider nos acquis en Java, j’ai réalisé durant ma deuxième année une application de gestion de stocks. Celle-ci, reliée à une API, permettait de rechercher et d\'obtenir des détails d’ajouter sur les films et séries.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['Java', 'Programmation Orientée Objet', 'Développement logiciel', 'Design Pattern'],
        },
        {
          id: 9,
          name: 'Train',
          description: 'Mise en place des différents design patterns pouvant servir à la gestion d\'un train',
          longDescription:'Afin d’appréhender la programmation orientée objet, nous avons du créer une application mettant en application toutes les notions de la programmation orientée objet.Le projet doté d’un menu, permet de customiser entièrement un train : de la direction de celui-ci en passant par le nombre de wagons.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['Java', 'Programmation Orientée Objet', 'Développement logiciel', 'Design Pattern'],
        },
        {
          id: 10,
          name: 'CRUD Vue.JS / Laravel ',
          description: 'Réalisation d\'un test technique mettant en oeuvre Vue 3 et une API sous Laravel',
          longDescription:'Ce projet m\'a permis d\'apprendre à utiliser les technologies que sont Vue.JS et Laravel et à approndir mes connaissances en POO et surtout en développement front.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['Vue.JS', 'Laravel', 'Développement web', 'API', 'MySQL'],
        },
        {
          id: 11,
          name: 'Simulation de feu de forêt',
          description: 'Réalisation d\'un test technique permettant de simuler visuellement un feu de forêt',
          longDescription:'Ce projet m\'a permis de faire du développement logiciel avec une réelle interface graphique, notion que je n\'avais pas pu aborder dans mon cursus scolaire.',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['Java', 'JavaFX', 'Développement logiciel', 'Interfaçage', 'Algorithmie'],
        },
        {
          id: 12,
          name: 'Equipe 17',
          description: 'Réalisation d\'une application de babyfoot connecté',
          longDescription:'Premier projet où j\'ai travaillé dans une équipe de 7 personnes. J\'y ai approfondi mes connaissances en Laravel',
          imageSrc: 'https://picsum.photos/200/300?random=1',
          technologies: ['Laravel', 'Développement web', 'Github', 'Travail en équipe'],
        },
      ],
      activeFilters: [],
      popupVisible: false,
      currentProject: {},
    }
  },
  computed: {
    filteredProjects() {
      if (this.activeFilters.length === 0) {
        return this.projects
      } else {
        return this.projects.filter(project => {
          return project.technologies.some(tech => this.activeFilters.includes(tech))
        })
      }
    }
  },
  methods: {
    toggleFilter(tech) {
      if (this.activeFilters.includes(tech)) {
        this.activeFilters.splice(this.activeFilters.indexOf(tech), 1)
      } else {
        this.activeFilters.push(tech)
      }
    },
    showPopup(project) {
      this.currentProject = project
      this.popupVisible = true
    },
  },
}

  </script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

.listingProject
{
 font-family: 'Montserrat', sans-serif !important;
}
</style>