<template>
    <div class="custom-table">
      <table>
        <thead>
          <tr>
            <th>Selecione</th>
            <th @click="ordenarPor('nome')" :class="{ 'asc': colunaOrdenada === 'nome' && ordemAscendente, 'desc': colunaOrdenada === 'nome' && !ordemAscendente }">Nome</th>
            <th @click="ordenarPor('email')" :class="{ 'asc': colunaOrdenada === 'email' && ordemAscendente, 'desc': colunaOrdenada === 'email' && !ordemAscendente }">Email</th>
            <th @click="ordenarPor('status')" :class="{ 'asc': colunaOrdenada === 'status' && ordemAscendente, 'desc': colunaOrdenada === 'status' && !ordemAscendente }">Status</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
            <tr v-for="(item, index) in items" :key="index">
            <td>
              <input type="checkbox" v-model="item.selecionado" />
            </td>
            <td>
              <input type="text" v-model="item.nome" :disabled="!item.editandoNome" />
            </td>
            <td>
              <input type="text" v-model="item.email" :disabled="!item.editandoEmail" />
            </td>
            <td>
              <input type="text" v-model="item.status" :disabled="!item.editandoStatus" />
            </td>
            <td>
              <button @click="editarItem(item)">Editar</button>
            </td>
          </tr>
        </tbody>
      </table>
      <button @click="excluirItensSelecionados"> Excluir </button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        items: [
          { nome: 'junior', email: 'junior@gmail.com', status: 'Ativo', editandoNome: false, editandoEmail: false, editandoStatus: false, selecionado: false },
          { nome: 'graciano', email: 'graciano@gmail.com', status: 'Inativo', editandoNome: false, editandoEmail: false, editandoStatus: false, selecionado: false },
          { nome: 'gracianojunior', email: 'jrgraciano@gmail.com', status: 'Inativo', editandoNome: false, editandoEmail: false, editandoStatus: false, selecionado: false }
        ],
        colunaOrdenada: '',
        ordemAscendente: true
      };
    },
    methods: {
      editarItem(item) {
        item.editandoNome = true;
        item.editandoEmail = true;
        item.editandoStatus = true;
      },
      excluirItem(index) {
        this.items.splice(index, 1);
      },
      excluirItensSelecionados() {
        this.items = this.items.filter(item => !item.selecionado);
      },
      ordenarPor(coluna) {
        if (this.colunaOrdenada === coluna) {
          this.ordemAscendente = !this.ordemAscendente;
        } else {
          this.ordemAscendente = true;
        }
  
        this.colunaOrdenada = coluna;
  
        this.items.sort((a, b) => {
          const valorA = a[coluna].toLowerCase();
          const valorB = b[coluna].toLowerCase();
          if (valorA < valorB) {
            return this.ordemAscendente ? -1 : 1;
          }
          if (valorA > valorB) {
            return this.ordemAscendente ? 1 : -1;
          }
          return 0;
        });
      }
    }
  };
  </script>
  
  <style>
    .asc::after {
      content: '↑';
    }
  
    .desc::after {
      content: '↓';
    }
  </style>
  