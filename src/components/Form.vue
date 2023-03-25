<template>
    <form class="bg-green-50 shadow-md rounded p-8 m-4">
        <!-- TimeLine -->
        <div class="flex justify-center mt-8">
          <div class="flex items-center">
            <button :class="{'bg-blue-500 text-white': currentStep >= 1}"
                    @click.prevent="changeStep(1)" 
                    class="bg-gray-200 
                            p-2
                            hover:bg-green-500
                            font-bold 
                            py-2 px-4 
                            rounded 
                            focus:outline-none 
                            focus:shadow-outline"> Paso 1 </button>
            <div :class="{'bg-blue-500': currentStep >= 2}"
                  class="bg-gray-300 p-2 rounded-full h-1 flex-1 ml-2"></div>
          </div>
          <div class="flex items-center ml-4">
            <button :class="{'bg-blue-500 text-white': currentStep >= 2}"
                    @click.prevent="changeStep(2)"
                    class="bg-gray-200 
                            p-2
                            hover:bg-green-500
                            font-bold 
                            py-2 px-4 
                            rounded 
                            focus:outline-none 
                            focus:shadow-outline"> Paso 2 </button>
            <div :class="{'bg-blue-500': currentStep >= 3}" 
                  class="bg-gray-300 p-2 rounded-full h-1 flex-1 ml-2"></div>
          </div>
          <div class="flex items-center ml-4">
            <button :class="{'bg-blue-500 text-white': currentStep >= 3}"
                    @click.prevent="changeStep(3)"
                    class="bg-gray-200 
                            p-2
                            hover:bg-green-500
                            font-bold 
                            py-2 px-4 
                            rounded 
                            focus:outline-none 
                            focus:shadow-outline"> Paso 3 </button>
          </div>
        </div>

        <!-- Form -->
        <div id="part1" v-show="currentStep == 1" class="grid grid-cols-3 gap-4 mt-8">
            <div
                v-for="(item, index) in dataInput1"
                :key="index"
                class="col-span-1"
            >
                <label class="block text-sm font-bold mb-2" :for="item.name">
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
        <div id="part2" v-show="currentStep == 2" class="grid grid-cols-3 gap-4 mt-10">
            <div
                v-for="(item, index) in dataInput2"
                :key="index"
                class="mb-3 basis-1/3"
            >
                <label class="block text-sm font-bold mb-2" :for="item.name">
                    {{ item.label }}
                </label>
                <div class="flex flex-row items-center">
                    <input
                        v-model="item.input"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        :class="{
                            'border-red-500': !item.valid && item.showError,
                        }"
                        :id="item.name"
                        :type="item.type"
                        :placeholder="item.placeholder"
                        @input="
                            validateInput2(index, item.name, $event.target.value)
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
        <div id="part3" v-show="currentStep == 3" class="grid grid-cols-2 gap-4 mt-10">
            <div
                v-for="(item, index) in dataInput3"
                :key="index"
                class="mb-3 basis-1/3"
            >
                <label class="block text-sm font-bold mb-2" :for="item.name">
                    {{ item.label }}
                </label>
                <div class="flex flex-row items-center">
                    <input
                        v-model="item.input"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                        :class="{
                            'border-red-500': !item.valid && item.showError,
                        }"
                        :id="item.name"
                        :type="item.type"
                        :placeholder="item.placeholder"
                        @input="
                            validateInput3(index, item.name, $event.target.value)
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

        <!-- send -->
        <div class="flex items-center justify-between mt-8">
            <button
                v-if="currentStep >= 3"
                @click.prevent="sendForm"
                class="ml-auto 
                      bg-blue-500 
                      hover:bg-blue-700 
                      text-white 
                      font-bold 
                      py-2 
                      px-4 
                      rounded 
                      focus:outline-none 
                      focus:shadow-outline"
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
                    label: "Correo Electrónico",
                    placeholder: "Email",
                    type: "text",
                    input: "",
                    valid: false,
                    showError: false,
                },
                {
                    name: "pwd",
                    label: "Contraseña",
                    placeholder: "Contraseña",
                    type: "password",
                    input: "",
                    valid: false,
                    showError: false,
                },
                {
                    name: "pwdConfirm",
                    label: "Confirmar contraseña",
                    placeholder: "Contraseña",
                    type: "password",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "telephone",
                    label: "Número de teléfono",
                    placeholder: "Teléfono",
                    type: "tel",
                    input: "",
                    valid: false,
                    showError: false,
                },{
                    name: "phone",
                    label: "Número de celular",
                    placeholder: "Celular",
                    type: "tel",
                    input: "",
                    valid: false,
                    showError: false,
                },
            ],
            dataInput3: [
              {
                name: "address",
                label: "Dirección de residencia",
                placeholder: "Dirección",
                type: "text",
                input: "",
                valid: false,
                showError: false,
              },
              {
                name: "postalCode",
                label: "Código postal",
                placeholder: "Código postal",
                type: "number",
                input: "",
                valid: false,
                showError: false,
              }
            ],
            currentStep: 1,
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
          if (this.dataInput1[index].showError == false)
                this.dataInput1[index].showError = true;

  
          if(name == 'pais' || name == "genero" || name == "typeDocument"){
            this.dataInput1[index].valid = true;
          }
          else if(name =="firstName" || name == "secondName"){
            if(input.length > 0)
              this.dataInput1[index].valid = true;
            else
              this.dataInput1[index].valid = false;
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
              console.log('El usuario es menor de edad');
            }
          }
          else if(name == "idDocument"){
            if(input.length >= 5) this.dataInput1[index].valid = true
            else this.dataInput1[index].valid = false
          }
          else if(name == "fileDocFront" || name == "fileDocBack"){
            if(/\.(jpg|jpeg)$/.test(input)) this.dataInput1[index].valid = true
            else this.dataInput1[index].valid = false
          }
        },
        validateInput2(index, name, input) {
            if (this.dataInput2[index].showError == false)
                this.dataInput2[index].showError = true;
            if (name == "email") {
                const regex = /\S+@\S+\.\S+/;
                this.dataInput2[index].valid = regex.test(input);
            }
            else if(name == "pwd"){
              if(input.length > 0)
                this.dataInput2[index].valid = true
              else
                this.dataInput2[index].valid = false
            }
            else if(name == "pwdConfirm"){
              if(input == this.dataInput2[index-1].input)
                this.dataInput2[index].valid = true
              else 
                this.dataInput2[index].valid = false
            }
            else if( name == "telephone") {
              if(/^\d{7}$/.test(input)) this.dataInput2[index].valid = true
              else this.dataInput2[index].valid = false
            }
            else if( name == "phone"){
              if(/^\d{10}$/.test(input)) this.dataInput2[index].valid = true
              else this.dataInput2[index].valid = false
            }
        },
        validateInput3(index, name, input){
            if (this.dataInput3[index].showError == false)
                this.dataInput3[index].showError = true;
            if(name == "address"){
              if(input.length > 0)
                this.dataInput3[index].valid = true
              else
                this.dataInput3[index].valid = false
            }
            else if (name == "postalCode"){
              if(/^\d{6}$/.test(input)) this.dataInput3[index].valid = true
              else this.dataInput3[index].valid = false
            }
        },
        sendForm() {
          // concateno todos los campos de cada paso en un solo array
          const data = this.dataInput1.concat(this.dataInput2,this.dataInput3)
            // envio la data al componente padre app.vue verificando que todos los campos esten completados
            if (data.every((e) => e.valid == true)) {
                this.$emit("submit", data);
            } else {
                this.dataInput3.map(e => e.showError = true)
            }
        },
        changeStep(number){
          if(this.currentStep == 1  && number == 2){
            if(this.dataInput1.every(e => e.valid == true)){
              this.currentStep = number
            }
            else
              this.dataInput1.map(e => e.showError = true)
          }
          else if(this.currentStep == 1  && number == 3){
            if(this.dataInput1.every(e => e.valid == true)){
              if(this.dataInput2.every(e => e.valid == true)){
                this.currentStep = number
              }
            } 
            else
              this.dataInput1.map(e => e.showError = true)
          }
          else if(this.currentStep == 2 && number == 3){
            if(this.dataInput2.every(e => e.valid == true))
              this.currentStep = number
            else
              this.dataInput2.map(e => e.showError = true)
          } else {
            this.currentStep = number
          }
        }
    },
};
</script>


<style>
</style>