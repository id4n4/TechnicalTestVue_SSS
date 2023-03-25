<template>
    <form class="bg-green-50 shadow-md rounded p-8 m-4">
        <div id="part1" class="grid grid-cols-3 gap-4">
            <div
                v-for="(item, index) in dataInput1"
                :key="index"
                class="col-span-1"
            >
                <label class="block text-sm font-bold mb-2" for="{{item.name}}">
                    {{ item.label }}
                </label>
                <div class="flex flex-row items-center">
                    <select
                        v-if="item.type == 'select'"
                        v-model="item.input"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        @change="validateInput1(index, item.name, $event.target.value)"
                    >
                        <option value="" disabled>
                            {{ item.placeholder }}
                        </option>
                        <option
                            v-for="(option,index) in item.data"
                            :key="index"
                            :value="option"
                        >
                            {{ option }}
                        </option>
                    </select>
                    <input
                        v-else
                        v-model="item.input"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        :class="{
                            'border-red-500': !item.valid && item.showError,
                        }"
                        :id="item.name"
                        :type="item.type"
                        :placeholder="item.placeholder"
                        @input="
                            validateInput1(index, item.name, $event.target.value)
                        "
                    />
                    <span
                        v-if="item.valid"
                        class="inline-block align-middle text-green-800"
                        >&#x2714;</span
                    >
                    <span
                        v-else-if="item.showError"
                        class="inline-block align-middle text-red-500"
                        >&#x2718;</span
                    >
                </div>
            </div>
        </div>
        <div id="part2" class="flex flex-row">
            <div
                v-for="(item, index) in dataInput2"
                :key="index"
                class="mb-3 basis-1/3"
            >
                <label class="block text-sm font-bold mb-2" for="{{item.name}}">
                    {{ item.label }}
                </label>
                <div class="flex flex-row items-center">
                    <input
                        v-model="item.input"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        :class="{
                            'border-red-500': !item.valid && item.showError,
                        }"
                        id="email"
                        type="email"
                        placeholder="Email"
                        @input="
                            validateInput(index, item.name, $event.target.value)
                        "
                    />
                    <span
                        v-if="item.valid"
                        class="inline-block align-middle text-green-800"
                        >&#x2714;</span
                    >
                    <span
                        v-else-if="item.showError"
                        class="inline-block align-middle text-red-500"
                        >&#x2718;</span
                    >
                </div>
            </div>
        </div>

        <div class="flex items-center justify-between">
            <button
                @click.prevent="sendForm"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                type="button"
            >
                Enviar
            </button>
        </div>
    </form>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
    data() {
        return {
            dataInput1: [
                {
                    name: "pais",
                    label: "País",
                    placeholder: "Selecciona un país",
                    type: "select",
                    data: [],
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "genero",
                    label: "Genero",
                    placeholder: "Selecciona tu genero",
                    type: "select",
                    data: ["Masculino","Femenino", "Otros"],
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "firstName",
                    label: "Primer nombre",
                    placeholder: "primer nombre",
                    type: "text",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "secondName",
                    label: "Segundo nombre",
                    placeholder: "Segundo nombre",
                    type: "text",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "birthdate",
                    label: "Fecha de Nacimiento",
                    type: "date",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "typeDocument",
                    label: "Tipo de documento",
                    placeholder: "Selecciona tipo de documento",
                    type: "select",
                    data: ["Cedula de ciudadanía","Pasaporte", "Cedula de extranjería"],
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "idDocument",
                    label: "Número de documento",
                    placeholder: "Selecciona Número de documento",
                    type: "number",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "fileDocFront",
                    label: "Foto documento - Frente",
                    placeholder: "Subir archivo",
                    type: "file",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "fileDocBack",
                    label: "Foto documento - Reverso",
                    placeholder: "Subir archivo",
                    type: "file",
                    input: "",
                    valid: false,
                    showError: false,
                },
                
            ],
            dataInput2: [
                {
                    name: "email",
                    label: "Email",
                    input: "",
                    valid: false,
                    showError: false,
                },
            ],
        };
    },
    mounted() {
        // Realiza la petición a la API para obtener los países
        axios
            .get("https://restcountries.com/v3.1/all")
            .then((response) => {
                // Asigna los países al array de countries para el select
                if (response) {
                    // Ordeno los paises por nombre
                    let data = response.data.sort((a, b) => {
                        if (a.name.common > b.name.common) {
                            return 1;
                        }
                        if (a.name.common < b.name.common) {
                            return -1;
                        }
                        return 0;
                    });
                    this.dataInput1[0].data = data.map(e=> {return e.name.common})
                }
            })
            .catch((error) => {
                console.log(error);
                console.log("holamundo");
            });
    },
    methods: {
        validateInput1(index,name,input){
          console.log(input)
          if(name == 'pais' || name == "genero" || name == "typeDocument"){
            this.dataInput1[index].valid = true;
          }
          else if(name == "birthdate"){
            const today = moment();
            const birthdate = moment(input);
            const age = today.diff(birthdate, 'years');
            if (age >= 18) {
              this.dataInput1[index].valid = true
              console.log('El usuario es mayor de edad');
            } else {
              this.dataInput1[index].valid = false
              this.dataInput1[index].showError = true
              console.log('El usuario es menor de edad');
            }
          }
          else if(name == "idDocument"){
            if(input.length >= 5) this.dataInput1[index].valid = true
            else {
              this.dataInput1[index].valid = false
              this.dataInput1[index].showError = true
            }
          }
          else if(name == "fileDocFront" || name == "fileDocBack"){
            if(/\.(jpg|jpeg)$/.test(input)) this.dataInput1[index].valid = true
            else {
              this.dataInput1[index].valid = false
              this.dataInput1[index].showError = true
            }
          }
        },
        validateInput2(index, name, input) {
            if (this.dataInput2[index].showError == false)
                this.dataInput2[index].showError = true;
            if (name == "email") {
                const regex = /\S+@\S+\.\S+/;
                this.dataInput2[index].valid = regex.test(input);
            }
        },
        sendForm() {
            // Aquí puedes guardar los datos del formulario en una base de datos o en un servidor
            // Luego, puedes mostrar los datos en un modal
            if (this.dataInput2.every((e) => e.valid == true)) {
                this.$emit("submit", this.dataInput2);
            } else {
                window.alert("error, don't working");
            }
        },
    },
};
</script>


<style>
</style>