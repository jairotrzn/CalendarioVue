<template>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
      <v-spacer></v-spacer>
      <template>
        <div class="text-center">
          <v-btn class="mx-2" fab dark color="indigo" @click="dialog = true">
            <v-icon dark>mdi-plus</v-icon>
          </v-btn>
        </div>
      </template>
    </v-card-title>
    <v-data-table :headers="headers" :items="machines" :search="search">
      <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" color="red" @click="deleteMachine(item)"
          >mdi-delete</v-icon
        >
        <v-icon small color="blue" @click="editDessert(item)"
          >mdi-pencil</v-icon
        >
      </template>
    </v-data-table>
    <!-- Modal Agregar Evento -->
    <v-dialog v-model="dialog">
      <v-card>
        <v-container>
          <v-form @submit.prevent="addMachine">
            <p><b>CARACTERISTICAS TÉCNICAS</b></p>

            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="text"
                  label="Agregar Tipo de maquina"
                  v-model="type"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="text"
                  label="Ubicacion"
                  v-model="location"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="text"
                  label="Código Máquina"
                  v-model="machineCode"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="text"
                  label="Departamento"
                  v-model="department"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Potencia Motor Principal (CV)"
                  v-model="mainMotorPower"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Potencia Motor Avances (CV)"
                  v-model="feedMotorPower"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Potencia Motobomba(CV)"
                  v-model="pumpMotorPower"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Corriente (V)"
                  v-model="current"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Velocidad Máxima (RPM)"
                  v-model="maximumSpeed"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Velocidad Mínima (RPM)"
                  v-model="minimumSpeed"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Nº de Velocidades"
                  v-model="numberOfSpeeds"
                ></v-text-field>
              </v-col>
            </v-row>
            <p><b>AVANCES MÁXIMOS</b></p>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Avance Máximo Longitudinal"
                  v-model="maximumLongitudinalFeed"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Nº avances longitudinales"
                  v-model="numberOfLongitudinalFeeds"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Avance Máximo Transversal"
                  v-model="maximumTransversalFeed"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Nº avances Transversal"
                  v-model="numberOfTransversalFeeds"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Avance Máximo Vertical"
                  v-model="maximumVerticalFeed"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Nº avances Vertical"
                  v-model="numberOfVerticalFeeds"
                ></v-text-field>
              </v-col>
            </v-row>
            <p><b>AVANCES MÍNIMOS</b></p>
            <v-row>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Avance Mínimo Longitudinal"
                  v-model="minimumLongitudinalFeed"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Avance Mínimo Transversal"
                  v-model="minimumTransversalFeed"
                ></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  type="number"
                  label="Avance Mínimo vertical"
                  v-model="minimumVerticalFeed"
                ></v-text-field>
              </v-col>
            </v-row>

            <v-file-input
              v-model="image"
              accept="image/*"
              label="Agregar una imagen"
            ></v-file-input>
            <v-btn
              type="submit"
              color="primary"
              class="mr-4"
              @click.stop="dialog = false"
              >Agregar</v-btn
            >
          </v-form>
        </v-container>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
import { updateDoc } from "firebase/firestore";
import { db, collection, getDocs, addDoc, deleteDoc, doc } from "../main";
export default {
  data() {
    return {
      search: "",
      dialog: false,
      machines:[],

      image: null,
      type: null,
      location: null,
      machineCode: null,
      department: null,
      mainMotorPower: null,
      feedMotorPower: null,
      pumpMotorPower: null,
      current: null,
      maximumSpeed: null,
      minimumSpeed: null,
      numberOfSpeeds: null,
      maximumLongitudinalFeed: null,
      numberOfLongitudinalFeeds: null,
      maximumTransversalFeed: null,
      numberOfTransversalFeeds: null,
      maximumVerticalFeed: null,
      numberOfVerticalFeeds: null,
      minimumLongitudinalFeed: null,
      minimumTransversalFeed: null,
      minimumVerticalFeed: null,


      headers: [
        {
          text: "Cod.Maquina",
          align: "start",
          filterable: false,
          value: "machineCode",
        },
        { text: "Tipo", value: "type" },
        { text: "Ubicación", align: "center", value: "location" },
        {
          text: "Potencia Motor Principal",
          align: "center",
          value: "mainMotorPower",
        },
        { text: "Velocidad Máxima", align: "center", value: "maximumSpeed" },
        { text: "Acciones", value: "actions" },
      ],

    };
  },
  created(){
    this.getMachines();
  },
  methods: {
    async deleteMachine(item){
      try {
        const docRef = doc(db,'machines',item.id);
        await deleteDoc(docRef);
        this.getMachines();
      } catch (error) {
        console.log(error)
      }
    },
    async getMachines(){
      try {
         const snapshot =await getDocs(collection(db, "machines"));
          const machines = [];
     
          snapshot.forEach(doc => {
            let machineData = doc.data();
            machineData.id = doc.id;
            machines.push(machineData);
          })

          this.machines = machines;
      } catch (error) {
        console.log(error)
      }
    },
    async addMachine() {
      try {
        if (
          (//this.image,
          this.type,
          this.location,
          this.machineCode,
          this.department,
          this.mainMotorPower,
          this.feedMotorPower,
          this.pumpMotorPower,
          this.current,
          this.maximumSpeed,
          this.minimumSpeed,
          this.numberOfSpeeds,
          this.maximumLongitudinalFeed,
          this.numberOfLongitudinalFeeds,
          this.maximumTransversalFeed,
          this.numberOfTransversalFeeds,
          this.maximumVerticalFeed,
          this.numberOfVerticalFeeds,
          this.minimumLongitudinalFeed,
          this.minimumTransversalFeed,
          this.minimumVerticalFeed)
        ) {
         
          await addDoc(collection(db, "machines"), {
           // image: this.image,
            type: this.type,
            location: this.location,
            machineCode: this.machineCode,
            department: this.department,
            mainMotorPower: this.mainMotorPower,
            feedMotorPower: this.feedMotorPower,
            pumpMotorPower: this.pumpMotorPower,
            current: this.current,
            maximumSpeed: this.maximumSpeed,
            minimumSpeed: this.minimumSpeed,
            numberOfSpeeds: this.numberOfSpeeds,
            maximumLongitudinalFeed: this.maximumLongitudinalFeed,
            numberOfLongitudinalFeeds: this.numberOfLongitudinalFeeds,
            maximumTransversalFeed: this.maximumTransversalFeed,
            numberOfTransversalFeeds: this.numberOfTransversalFeeds,
            maximumVerticalFeed: this.maximumVerticalFeed,
            numberOfVerticalFeeds: this.numberOfVerticalFeeds,
            minimumLongitudinalFeed: this.minimumLongitudinalFeed,
            minimumTransversalFeed: this.minimumTransversalFeed,
            minimumVerticalFeed: this.minimumVerticalFeed,
          });
          this.getMachines();
          inizialite();
        } else {
          console.log("los campos estan vacios");
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};

function inizialite(){
        image: null;
      type: null;
      location: null;
      machineCode: null;
      department: null;
      mainMotorPower: null;
      feedMotorPower: null;
      pumpMotorPower: null;
      current: null;
      maximumSpeed: null;
      minimumSpeed: null;
      numberOfSpeeds: null;
      maximumLongitudinalFeed: null;
      numberOfLongitudinalFeeds: null;
      maximumTransversalFeed: null;
      numberOfTransversalFeeds: null;
      maximumVerticalFeed: null;
      numberOfVerticalFeeds: null;
      minimumLongitudinalFeed: null;
      minimumTransversalFeed: null;
      minimumVerticalFeed: null;
}
function camposVacios(
  //image,
  type,
  location,
  machineCode,
  department,
  mainMotorPower,
  feedMotorPower,
  pumpMotorPower,
  current,
  maximumSpeed,
  minimumSpeed,
  numberOfSpeeds,
  maximumLongitudinalFeed,
  numberOfLongitudinalFeeds,
  maximumTransversalFeed,
  numberOfTransversalFeeds,
  maximumVerticalFeed,
  numberOfVerticalFeeds,
  minimumLongitudinalFeed,
  minimumTransversalFeed,
  minimumVerticalFeed
) {
  if (
   // image === "" ||
    type === "" ||
    location === "" ||
    machineCode === "" ||
    department === "" ||
    mainMotorPower === "" ||
    feedMotorPower === "" ||
    pumpMotorPower === "" ||
    current === "" ||
    maximumSpeed === "" ||
    minimumSpeed === "" ||
    numberOfSpeeds === "" ||
    maximumLongitudinalFeed === "" ||
    numberOfLongitudinalFeeds === "" ||
    maximumTransversalFeed === "" ||
    numberOfTransversalFeeds === "" ||
    maximumVerticalFeed === "" ||
    numberOfVerticalFeeds === "" ||
    minimumLongitudinalFeed === "" ||
    minimumTransversalFeed === "" ||
    minimumVerticalFeed === ""
  ) {
    return true;
  } else {
    return false;
  }
}
</script>
