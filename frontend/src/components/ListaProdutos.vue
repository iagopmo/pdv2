<template> 
    <div class="container mt-4">
        <table class="table">
          <thead>
            <tr>
              <th>Nome</th>
              <th>Preço de Custo</th>
              <th>Preço de Venda</th>
              <th>Tipo</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="produto in produtos" :key="produto.id">
              <td>
                <span v-if="!editando">{{ produto.nomeproduto }}</span>
                <input v-else v-model="produto.nomeproduto" />
              </td>
              <td>
                <span v-if="!editando">{{ produto.preco_custo }}</span>
                <input v-else v-model="produto.preco_custo" />
              </td>
              <td>
                <span v-if="!editando">{{ produto.preco_venda }}</span>
                <input v-else v-model="produto.preco_venda" />
              </td>
              <td>
                <span v-if="!editando">{{ produto.nometipoproduto }}</span>
                <select v-else v-model="produto.tipo_produto_id">
                  <option value="1">Fruta</option>
                  <option value="2">Legumes</option>
                  <option value="3">Verdura</option>
                  <option value="4">Carne</option>
                  <option value="5">Laticínios</option>
                  <option value="6">Bebidas</option> 
                </select>
              </td>
              <td>
                <div class="btn-group" role="group" aria-label="Opções">
                    <button v-if="!editando" type="button" class="btn btn-primary" @click="editProduto">Editar</button>
                    <template v-else>
                        <button type="button" class="btn btn-success" @click="salvarProduto(produto)">Salvar</button>
                    </template>
                    <button type="button" class="btn btn-danger" @click="deleteProduto(produto)">Deletar</button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>    
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            produtos: [],
            editando: false
        }        
    },
    mounted() {
        axios.get('http://localhost:8080/listarProdutos').then(response => {            
            this.produtos = response.data;
            this.editando = false;
        }).catch(error => {
            console.log("Erro ao carregar dados do produto" + error);
        })
    },
    methods: {
        editProduto(){
          console.log(this.editando);
          // this.editando = true;
          return this.editando = !this.editando;
        },
        salvarProduto(produto){
            console.log(produto);
        }
    }
}
</script>

<style>

</style>