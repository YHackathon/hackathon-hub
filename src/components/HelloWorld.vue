<template>
   <v-container id="projects" class="listingProject">
    <v-app>
    <v-app-bar app color="indigo" dark>
      <v-toolbar-title>Faux SoundPlayer</v-toolbar-title>

      <v-spacer></v-spacer>

      <!-- Faux SoundPlayer Controls -->
      <v-btn icon>
        <v-icon>mdi-skip-previous</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-play</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-pause</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-skip-next</v-icon>
      </v-btn>

      <v-slider
        class="mx-4"
        v-model="soundLevel"
        :max="100"
        step="1"
        hide-details
        small
      ></v-slider>

      <v-btn icon @click="toggleMute">
        <v-icon>{{ isMuted ? 'mdi-volume-off' : 'mdi-volume-high' }}</v-icon>
      </v-btn>
    </v-app-bar>
  </v-app>




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
            <v-chip v-for="tech in project.technologies" :key="tech" class='bg-mediumblue mr-4'>{{ tech }}</v-chip>
            <v-btn width="100%" class="mt-3" color="deepblue" :href="project.link">
            Découvrir le projet
          </v-btn>

          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
<script>
  export default {
  data() {
    return {
      soundLevel:30, 
      isMuted: false,
      filters: ['Web', 'Jeu en ligne', 'Mobile', 'Jeu vidéo', 'Multijoueur','Logiciel'],
      projects: [
        {
          id: 1,
          name: 'YDiscover',
          link : 'https://main.dmnepnuwu4hll.amplifyapp.com/',
          description: 'Création d\'un site de recommandations d\'artistes et génération de fond d\'écran en fonction des albums les plus streamés.',
          imageSrc: 'src/assets/bg_card/project_1.PNG',
          technologies: ['Web'],
        },
        {
          id: 2,
          name: 'YMusic',
          link : '/',
          description: 'Création d\'un IDE pour jouer de la musique. Codez pour générer des sons qui seront interprétés par notre outil.',
          imageSrc: 'https://www.optimoz.fr/wp-content/uploads/2018/05/404-not-found-error-.jpg',
          technologies: ['Web'],
        },
        {
          id: 3,
          name: 'YLocoTunes',
          link : 'https://bechamelloww.github.io/vitrine-YLocoTunes/#mvpH',
          description: 'Application web de découverte d\'artistes locaux et exploration des événements musicaux locaux.',
          imageSrc: 'src/assets/bg_card/project_3.PNG',
          technologies: ['Web'],
        },
        {
          id: 4,
          name: 'SoundSphere',
          link : 'https://soundsphere.gcristini.fr/',
          description: 'SoundSphere est une application mobile qui permet de créer une file d\'attente musicale collaborative.',
          imageSrc: 'src/assets/bg_card/project_4.PNG',
          technologies: ['Mobile', 'Multijoueur'],
        },
        {
          id: 5,
          name: 'Swopy',
          link : 'https://vitrine.swopy.fun/',
          description: 'Application web qui permet de créer une file d\'attente musicale entre amis avec un système de vote par popularité.',
          imageSrc: 'src/assets/bg_card/project_5.PNG',
          technologies: ['Web', 'Multijoueur'],
        },
        {
          id: 6,
          name: 'YQuizz',
          link : 'https://hackathon-23-24-equipe6.github.io/vitrine//',
          description: 'Application de quizz en ligne permettant de tester ses connaissances sur les différents genres musicaux.',
          imageSrc: 'src/assets/bg_card/project_6.PNG',
          technologies: ['Web', 'Jeu en ligne'],
        },
        {
          id: 7,
          name: 'Harmonifund',
          link : 'https://vitrine-harmonifund.netlify.app/',
          description: 'Participez aux campagnes de financement participatif pour soutenir vos artistes préférés !',
          imageSrc: 'src/assets/bg_card/project_7.PNG',
          technologies: ['Web'],
        },
        {
          id: 8,
          name: 'QuizTune',
          link : 'https://dancing-crumble-390602.netlify.app/',
          description: 'Plateforme de quizz en temps réel en multijoueurs sous forme d\'extraits musicaux ou de lyrics à reconnaître.',
          imageSrc: 'src/assets/bg_card/project_8.PNG',
          technologies: ['Web', 'Jeu en ligne', 'Multijoueur'],
        },
        {
          id: 9,
          name: 'OST-Museum',
          link : 'https://ost-museum-web.vercel.app/',
          description: 'Musée interactif où vous pourrez écouter les différents soundtracks de films, jeux vidéo et bien d\'autres encore !',
          imageSrc: 'src/assets/bg_card/project_9.PNG',
          technologies: ['Jeu vidéo'],
        },
        {
          id: 10,
          name: 'SonoSync',
          link : 'https://thomastiraboschi.github.io/Site-Vitrine-SonoSync/',
          description: 'Incarnez un agent d\'entretien dans un labyrinthe de défis et d\'énigmes rythmé par la musique diffusée par un poste radio aux pouvoirs suprenants.',
          imageSrc: 'src/assets/bg_card/project_10.PNG',
          technologies: ['Jeu vidéo'],
        },
        {
          id: 11,
          name: 'BeatTheBeat',
          link : 'https://hackathon-btb-vitrine.netlify.app/',
          description: 'Testez vos connaissances à travers des énigmes sonores, défiez vos amis en temps réel et découvrez de nouveaux genres et artistes.',
          imageSrc: 'src/assets/bg_card/project_11.PNG',
          technologies: ['Web', 'Multijoueur', 'Jeu en ligne'],
        },
        {
          id: 12,
          name: 'Solf\'ez',
          link : 'https://annegnoemie.github.io/solfez/',
          description: 'Vous avez toujours voulu apprendre à jouer au piano mais ne savez pas par où commencer ? Vous voulez améliorer votre oreille musicale ?',
          imageSrc: 'src/assets/bg_card/project_12.PNG',
          technologies: ['Web'],
        },
        {
          id: 13,
          name: 'Soundle',
          link : 'https://gaspardcs.fr/pages/accueil.html',
          description: 'Jeu vidéo explorant les différents gameplay d\'un jeu 2D en exploitant les effets sonores !',
          imageSrc: 'https://www.optimoz.fr/wp-content/uploads/2018/05/404-not-found-error-.jpg',
          technologies: ['Web', 'Jeu en ligne'],
        },
        {
          id: 14,
          name: 'YFestival',
          link : '/',
          description: 'Application web de gestion de festival avec informations sur les artistes et transports.',
          imageSrc: 'https://www.optimoz.fr/wp-content/uploads/2018/05/404-not-found-error-.jpg',
          technologies: ['Web'],
        },
        {
          id: 15,
          name: 'YMusic',
          link : 'https://ymusic2023.netlify.app/',
          description: 'Blind test en ligne sous la forme d\'un pendu. Tapez les lettres pour découvrir le son !',
          imageSrc: 'src/assets/bg_card/project_15.PNG',
          technologies: ['Web','Jeu en ligne'],
        },
        {
          id: 16,
          name: 'YError',
          link : 'https://ynov-hackathon-groupe-16.netlify.app/',
          description: 'Extension VS Code musicale de détection d\'erreurs de syntaxe sur différents langages.',
          imageSrc: 'src/assets/bg_card/project_16.PNG',
          technologies: ['Logiciel'],
        },
        {
          id: 17,
          name: 'MusiClash',
          link : 'https://34.71.240.139/',
          description: 'Application web de blind test en multijoueur local.',
          imageSrc: 'src/assets/bg_card/project_17.PNG',
          technologies: ['Web', 'Jeu en ligne', 'Multijoueur'],
        },
        {
          id: 18,
          name: 'Beathoven',
          link : 'https://beathoven-bot.netlify.app/',
          description: 'Bot Discord vous permettant de transformer vos messages en bande sonore.',
          imageSrc: 'src/assets/bg_card/project_18.PNG',
          technologies: ['Logiciel'],
        },
        {
          id: 19,
          name: 'Harmon IA',
          link : 'https://kaleidoscopic-valkyrie-fb1af0.netlify.app/',
          description: 'Application web d\'anlyse de fichiers musicaux et de retranscription de paroles de musique.',
          imageSrc: 'src/assets/bg_card/project_19.PNG',
          technologies: ['Web'],
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