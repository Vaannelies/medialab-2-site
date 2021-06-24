<template>
 <div class="about" style="height: 100vh;">
    <div  :style="headerStyles" class="header">
      <img class="logo" src="https://www.nieuwsbrievenrotterdam.nl/images/logo_gemeente_rotterdam_2021.png" alt="Logo van de Gemeente Rotterdam"/>
      <div class="mijn-loket">
        <img class="icon" src="../../public/img/icons/desktop-icon-loket.png" alt="Icoon van mijn loket"/>
        Mijn Loket
      </div>
       <select class="dropdown" id="languages" name="language">
        <option value="nl">NL</option>
        <option value="en">EN</option>
      </select>
    </div>
    <div  :style="headerStyles" class="header">
      <span class="login">
        <p id="name">Ingelogd als A. de Groot</p> | <p id="logout">uitloggen</p>
      </span>
    </div>
    <div class="body">
      <div class="text" :style="textStyles">
        <h1>Welkom, mevrouw de Groot</h1>
        <p :style="pStyles"><b>U heeft een afspraak op:</b><br>25 juni 2021 om 10:30 uur</p>
        <p  :style="pStyles"><b>Ambtenaar:</b><br>Mr. E. Traag</p>
      </div>

      <button :style="buttonStyles">
         <img class="icon--phone" src="../../public/img/icons/icon_start_call@2x.png" alt="Icoon van telefoon"/>
        Gesprek starten
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import  firebase from "firebase/app";
import "firebase/database"
@Component({
  components: {

  },
  computed: {
    textStyles() {
      return {
        "background-color": "this.bgColor",
        fontSize: `${this.colorValue}px`,
        height: 'fit-content',
      };
    },
    pStyles() {
      return {
        "background-color": "this.bgColor",
        fontSize: `${this.colorValue*1.4}px`,
        height: 'fit-content',
      };
    },
    headerStyles() {
      return {
        "background-color": "this.bgColor",
        fontSize: `${this.colorValue*0.6}px`,
      };
    },
    imageStyles() {
      return {
        "background-color": "this.bgColor",
        height: `${this.colorValue*1.2}px`,
        maxWidth: '800px'
      };
    },
    buttonStyles() {
      return {
        "background-color": "this.bgColor",
        fontSize: `${this.colorValue*1.2}px`,
        maxWidth: '800px'
      };
    }
  }
})
export default class About extends Vue {
  colorValue: any = 0;
  database: any;
  firebaseConfig: any = {
    apiKey: "AIzaSyBOvdEMkQvHeWEYj0LKN69PMdldRBkuR54",
    authDomain: "medialab-76b30.firebaseapp.com",
    databaseURL: "https://medialab-76b30-default-rtdb.firebaseio.com",
    projectId: "medialab-76b30",
    storageBucket: "medialab-76b30.appspot.com",
    messagingSenderId: "1059196583141",
    appId: "1:1059196583141:web:8c85ffb31e6dc1f0a2280c"
  };

     childs: [] = [];
  async created() {

if (!firebase.apps.length) {
    firebase.initializeApp(this.firebaseConfig);
}else {
   firebase.app(); // if already initialized, use that one
}

  firebase.database().ref("/booth").child("/color").on('value', (snapshot) => {
      snapshot.forEach((child) => {
        this.childs.push(
        )
      })
    })
    this.database = firebase.app().database();

    await this.fetchData();
  }

  // Get a reference to the database service


  async fetchData() {
    this.database = firebase.database()
    const ref = this.database.ref("/booth/color");

    ref.on('value', (snapshot) => {
      console.log(snapshot.val());

      this.colorValue = snapshot.val()/1023 * 100
      // this.colorValue = 100/snapshot.val();
    }, (errorObject) => {
      console.log("the read failed: ", errorObject.name);
    })
  }

}
</script>

<style lang="less" scoped>

  .about {
    background: black;
height: fit-content;
  }
  .header {
    height: 40px;
    padding: 20px;
    background: black;
    border-bottom: solid 1px white;
    display: flex;
    position: relative;
    align-items: center;

    ul {
      width: 50%;
      max-width: 600px;
      list-style: none;
      display: flex;
      color: white;
      li {
        margin-right: 20px;
      }
    }

    .login {
        line-height: 1em;
        display: flex;
        position: absolute;
        color: white;
        right: 50px;
        // font-size: 14px;
        #name {
          margin: 0;
          margin-right: 15px;
        }
        #logout {
          margin: 0;
          margin-left: 15px;
        }
    }

    .mijn-loket {
      color: white;
      // height: 100%;
      border:  1px solid white;
      border-bottom: none;
      // border-radius: 8px;
      padding: 10px 20px;
      position: absolute;
      right: 120px;
      line-height: 2em;
      bottom: 0;

      // height: 100%;
      // background: yellow;
    }
  }

      .icon {
        transform: translate(0, 25%);
        padding-right: 10px;
        &--phone {
          padding-right: 20px;
          transform: translate(0,25%);
          height: 2em;
        }
      }
  .body {
    display: flex;
    // justify-content: center;
    flex-direction: row;
    // align-items: center;
    justify-content: space-between;
    height: fit-content;
  //  height: 100vh;
    background: black;
    color: white;
    padding: 50px;
  }

  .text {
    background: black;
    display: flex;
    margin-left: 50px;
    flex-direction: column;
    justify-content: space-evenly;
    
  }
  .logo {
    width: 200px;
    height: 100%;
    filter:grayscale() brightness(500%);
    // position: absolute;
    // top: 30px;
    // left: 30px;
  }

  .dropdown {
    background: black;
    // border: 1px solid white;
    border: none;
    color: white;
    font-size: 20px;
    // top: 0;
    position: absolute;
    right: 40px;
  }

  .speaker-icon {
    position: absolute;
    bottom: 30px;
    right: 30px;
    height: 30px;
  }
// @import "./style.scss";

  button {
    color: white;
    background: black;
    padding: 5px 30px;
    height: fit-content;
    border-radius: 8px;
    line-height: 3em;
    font-size: 20px;
  }
// .text {
//   height: var(colorValue);
// }
  h1 {
    margin-top: 0;
    text-align: left;
    display: block;
    height: fit-content;
  }

  p {
  
    text-align: left;
    height: fit-content;
  }
</style>
