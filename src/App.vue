<template>
  <Header :header="this.header" />
  <div class="content-container">
    <section class="section-container" id="missions" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/mission-icon.svg" />
        <h1>Mission Log</h1>
      </div>
      <div class="section-content-container">
        <h3>Current Assignment</h3>
        <Markdown :source="current_md" class="markdown" />
        <h3>Mission List</h3>
        <div class="mission-list-container">
          <Mission
            v-for="item in this.missions"
            :key="item.slug"
            :mission="item"
            :selected="this.mission_slug"
            @click="selectMission(item)"
          />
        </div>
      </div>
    </section>
    <section class="section-container" id="events" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/events-icon.svg" />
        <h1>Events Log</h1>
      </div>
      <div class="section-content-container">
        <Markdown :source="events" class="markdown" />
      </div>
    </section>
    <section class="section-container" id="pilots" style="width:894px; height:714px;">
      <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Pilot Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
      </div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Pilot v-for="item in this.pilots" :key="item.slug" :pilot="item" />
        </div>
      </div>
    </section>
  </div>
  <svg
    style="visibility: hidden; position: absolute;"
    width="0"
    height="0"
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
  >
    <defs>
      <filter id="round">
        <feGaussianBlur in="SourceGraphic" stdDeviation="5" result="blur" />
        <feColorMatrix
          in="blur"
          mode="matrix"
          values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -5"
          result="goo"
        />
        <feComposite in="SourceGraphic" in2="goo" operator="atop" />
      </filter>
    </defs>
  </svg>
  <audio autoplay>
    <source src="/startup.ogg" type="audio/ogg" />
  </audio>
  <Footer/>
</template>

<script>
import Header from './components/layout/Header.vue';
import Footer from './components/layout/Footer.vue';
import Mission from './components/Mission.vue';
import Pilot from './components/Pilot.vue';
import Markdown from 'vue3-markdown-it';

export default {
  components: {
    Header,
    Footer,
    Mission,
    Pilot,
    Markdown
  },

  data() {
    return {
      "mission_slug": "001",
      "current_md": "",
      "events": "",
      "missions": [
        {
          "slug": "000",
          "name": "Shuttle Rubble",
          "status": "partial-success"
        },
        {
          "slug": "001",
          "name": "If the Suit Fits",
          "status": "start"
        },
      ],
      "pilots": [
        {
          "callsign": "Redcoat",
          "alias": "Reginald Eval",
          "code": "SNDRLIE-AXM-YTN-POS-HCP-OOA-ENR///SCYTALE-8-CONCORDIA//SECRPNA-AIP-RXE-ETS-POP-HEA-OSR",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Spitfire"
        },
        {
          "callsign": "Phoenix",
          "alias": "Ava Kalos",
          "code": "talae_cl_nfos_slfet_ehe_webi_dtaf///REDEFENSE-HARD-METALCORE//-e-edtatfeo-rslarocwltbafh-e-ls",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Nano"
        },
        {
          "callsign": "Caviar",
          "alias": "Abdulmalik Simmons",
          "code": "H-teoa-f-l-Vetaahureln-teMsde///TM-DHIYED//Trelorahe-rwtbra--nepydovSeene-hn-if",
          "corpro": "GMS",
          "frame": "Chomolungma",
          "mech": "Weight of the World"
        },
        {
          "callsign": "Fullmoon",
          "alias": 'Radojka "Rad-man" Androlewicz',
          "code": "I-dnIntw-SvproNrei--s-gPeoof_epkr///TM-DAWNLINE-SHORE//Bfibs-er--authuyesastemt-cr-t-areisoemi",
          "corpro": "GMS",
          "frame": "Sagarmatha",
          "mech": "Space Cowboy"
        },
        {
          "callsign": "Grim",
          "alias": "Xiang Juan Sweeting",
          "code": "I-w-m-oeelhit-thsemnt-eenishoc-o///TM-LUDRA-STONE//T-tf-ofeiU-eftnblu-gellmrnosyaew",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "A Good Example"
        },
        {
          "callsign": "Myrmidon",
          "alias": "Anicet Michelet-Dejardin",
          "code": "I-rihtlortslpa-aipKolwu-t--st-e///TM-BOUNDARY-GARDEN//T-lglnaifs-uoatc--eesgunoeHv-ar-eoh",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Mercy Clause"
        },
        {
          "callsign": "Samrat",
          "alias": "Amedee Sanmiguel",
          "code": "Ie-nr-dHiic-easatrniuhc-sseyC///TM-TBK-SOLO-TERRA//Io-n--tdtdh-reeUis-netSidreo-ocntyo",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Dangerous But Not Unbearably So"
        },
        {
          "callsign": "Sapphire",
          "alias": "Kari Bacho",
          "code": "It-suttw-mneyub-s-hrolmo-n-ytyd--HeroaiMi///TM-BOUNDARY-GARDEN//Aoc-Sdt-bsRoentaH--oneeUl-d-uOtm",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Unforeseen Impossibilities"
        },
        {
          "callsign": "Ichtaca",
          "alias": "???",
          "code": "Tl-wuhlthte-hoeyso---lsruwaeesiy-f///CAUSALITY-METAFOLD-SPACE//W--wsriisc-epthunlseoh-rhomsle-nowao-e",
          "corpro": "7h3yc0d3d17",
          "frame": "53cr3tzbyc411s16ns",
          "mech": "the404"
        },
      ],
      "header": {
        "planet": "Deep Space",
        "year": "5007u",
        "system": "Ardennes-3",
        "gate": "Atlas-Quanokrim",
        "ring": "Atlas-Line",
        "headerTitle": "Trunk Monkey",
        "headerSubtitle": "Company",
        "subheaderTitle": "Crisis Response",
        "subheaderSubtitle": "Papa-oscar-Echo",
      },
      "options":{
        "eventsMarkdownPerMission": true
      }
    }
  },

  created() {
    this.loadMissionMarkdown()
    this.loadEventsMarkdown()
  },

  computed: {

  },

  methods: {
    selectMission(mission) {
      this.mission_slug = mission.slug;
      this.loadMissionMarkdown()
      if(this.options.eventsMarkdownPerMission){
        this.loadEventsMarkdown();
      }
    },
    loadMissionMarkdown() {
      let self = this;
      let md = `/missions/${self.mission_slug}.md`
      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.current_md = client.responseText;
      }
      client.send();
    },
    loadEventsMarkdown() {
      let self = this;
      let md = "";

      if(self.options.eventsMarkdownPerMission){
        md = `/events/${self.mission_slug}.md`
      }
      else {
        md = "/events.md"
      }

      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.events = client.responseText;
      }
      client.send();
    }
  }

}
</script>


<style lang="scss">
#app {
  width: 1902px;
  height: 910px;
  overflow: hidden;
}
</style>
