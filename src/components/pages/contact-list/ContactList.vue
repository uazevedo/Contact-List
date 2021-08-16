<template>
  <v-container elevation="3">
    <v-row>
      <v-col cols="6" offset="3">
        <v-sheet 
        class="pa-5"
        elevation="3">
        <h1>Contatos
          <router-link 
          to="/about"
          custom
          >
            <v-btn 
            fab 
            small 
            dark 
            color="indigo" 
            class="my-5 float-end"
            name="new"
            >
              <v-icon>mdi-plus</v-icon>
            </v-btn>
          </router-link>
        </h1>

        <v-text-field 
        v-model="search"
        @input="searchContact(search)"
        prepend-icon="mdi-magnify"
        placeholder="Pesquisar" 
        type="text" class="my-5"></v-text-field>
        
        <v-card class="mx-auto">
          <v-list v-for="(contact, i) in filteredContacts" :key="i">
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>
                  {{ contact.name }} <v-btn icon class="float-end" @click="deleteContact(contact)"><v-icon color="red"> mdi-delete </v-icon></v-btn>
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>

            <v-list-item-content>
              <v-list>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon color="primary"> mdi-phone </v-icon>
                  </v-list-item-icon>
                  <!-- @mouseover="phoneNumber.hovered = true" @mouseleave="phoneNumber.hovered = false" -->
                  <v-list-item-content>
                    <template v-for="phoneNumber in contact.phoneNumbers">
                      <v-list-item-title :key="phoneNumber.number" v-if="phoneNumber">
                        {{ phoneNumber.number }}
                        <v-icon color="red" class="float-end" @click="deletePhoneNumber(contact, phoneNumber)"> mdi-close </v-icon>
                      </v-list-item-title>
                      <v-list-item-subtitle :key="phoneNumber.type">
                        {{ phoneNumber.type }}
                      </v-list-item-subtitle>
                    </template>
                  </v-list-item-content>
                </v-list-item>

                <v-divider inset></v-divider>

                <v-list-item v-if="contact.email">
                  <v-list-item-icon>
                    <v-icon color="primary"> mdi-email </v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>
                      {{ contact.email }}
                      <v-icon color="red" class="float-end"  @click="deleteEmail(contact)"> mdi-close </v-icon>
                    </v-list-item-title>
                    <v-list-item-subtitle> Mail </v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>

                <v-divider inset></v-divider>

                <v-list-item v-if="contact.address">
                  <v-list-item-icon>
                    <v-icon color="primary"> mdi-map-marker </v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>
                      {{ contact.address.street }}
                        <v-icon color="red" class="float-end" @click="deleteAddress(contact)"> mdi-close </v-icon>
                    </v-list-item-title>
                    <v-list-item-subtitle>
                      {{ contact.address.city }},
                      {{ contact.address.postalCode }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>

                <v-divider></v-divider>

              </v-list>
            </v-list-item-content>
          </v-list>
        </v-card>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: ['newContact'],
  data: function () {
    return {
      search:'',
      filteredContacts:[],
      contacts: [
        {
          name: "Ullisses Santos Neves Azevedo",
          email: "ullisses.neves@gmail.com",
          address: {
            street: "Av. José Conrado de Araújo, 116",
            city: "Aracaju",
            postalCode: "49065-470",
          },
          phoneNumbers: [
            { number: "(79)98809-9347", type: "Mobile" },
            { number: "(79)3227-4328", type: "Work" },
          ],
        },
        {
          name: "Thiago Squid",
          email: "thiago.squid@gmail.com",
          address: {
            street: "Aruana lá longe",
            city: "Aracaju",
            postalCode: "49999-411",
          },
          phoneNumbers: [
            { number: "(79)98851-6225", type: "Mobile" },
          ],
        },
        {
          name: "Ramon Félix Caiu do Avião",
          email: "ramom.voador@gmail.com",
          address: {
            street: "Rua do carinha que mora logo ali",
            city: "Aracaju",
            postalCode: "157",
          },
          phoneNumbers: [
            { number: "(79)99962-0470", type: "Mobile" }
          ],
        },
        {
          name: "Hélio Quatrocentos e Quarenta e Quatro",
          email: "hpfilho@gmail.com",
          address: {
            street: "Algum lugar depois da ponte",
            city: "Aracaju",
            postalCode: "444-444",
          },
          phoneNumbers: [
            { number: "(79)98120-8027", type: "Mobile" }
          ],
        },
        {
          name: "Teste 1",
          email: "teste1@gmail.com",
          address: {
            street: "Algum lugar depois da ponte",
            city: "Aracaju",
            postalCode: "444-444",
          },
          phoneNumbers: [
            { number: "(79)98120-8027", type: "Mobile" }
          ],
        },
        {
          name: "Teste 2",
          email: "teste2@gmail.com",
          address: {
            street: "Algum lugar depois da ponte",
            city: "Aracaju",
            postalCode: "444-444",
          },
          phoneNumbers: [
            { number: "(79)98120-8027", type: "Mobile" }
          ],
        },
        {
          name: "Teste 3",
          email: "teste3@gmail.com",
          address: {
            street: "Algum lugar depois da ponte",
            city: "Aracaju",
            postalCode: "444-444",
          },
          phoneNumbers: [
            { number: "(79)98120-8027", type: "Mobile" }
          ],
        },
      ],
    };
  },
  methods:{
    searchContact(searchText){
      if(searchText || searchText !== '')
        this.filteredContacts = this.contacts.filter(element => element.name.toLowerCase().includes(searchText.toLowerCase()))
      else
        this.filteredContacts = this.contacts
    },
    deleteContact(delContact){
      this.contacts = this.contacts.filter(contact => contact != delContact);
      this.filteredContacts = this.contacts
    },
    deletePhoneNumber(contact,phoneNumber){
      contact.phoneNumbers = contact.phoneNumbers.filter(number => number != phoneNumber);
    },
    deleteEmail(contact){
      contact.email = null;
    },
    deleteAddress(contact){
      contact.address = null;
    }
  },
  mounted(){
    this.filteredContacts = this.contacts
  }
};
</script>

<style>
</style>