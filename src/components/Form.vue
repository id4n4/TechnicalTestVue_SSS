<template>
    <form class="bg-blue-100 shadow-md rounded p-8 m-4">
        <div class="part1 flex flex-row">

            <div v-for="(item,index) in dataInput" :key="index" class="mb-3 basis-1/3">
                <label class="block text-sm font-bold mb-2" for="{{item.name}}">
                    {{item.Label}}
                </label>
                <div class="flex flex-row items-center">
                  <input
                      v-model="item.input"
                      class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                      :class="{'border-red-500': !item.valid && item.showError}"
                      id="email"
                      type="email"
                      placeholder="Email"
                      @input="validateInput(index, item.name,$event.target.value)"
                  />
                  <span
                      v-if="item.valid"
                      class="inline-block align-middle text-green-800"
                      >&#x2714;</span
                  >
                  <span v-else-if="item.showError" class="inline-block align-middle text-red-500"
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
export default {
    data() {
        return {
            dataInput:[
              {
                name: 'email',
                Label: "Email",
                input: '',
                valid: false,
                showError: false
              },
            ],
        };
    },
    methods: {
        validateInput(index, name, input) {
          if(this.dataInput[index].showError == false) this.dataInput[index].showError = true
          if(name=="email"){
            const regex = /\S+@\S+\.\S+/
            this.dataInput[index].valid = regex.test(input)
          }
        },
        sendForm() {
            // Aquí puedes guardar los datos del formulario en una base de datos o en un servidor
            // Luego, puedes mostrar los datos en un modal
            if(this.dataInput.every(e => e.valid == true)){
              this.$emit("submit", this.dataInput);

            } else {
              window.alert("error, don't working")
            }
        },
    },
};
</script>


<style>
</style>