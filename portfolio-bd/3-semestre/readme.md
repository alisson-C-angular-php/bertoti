# ⏱️ Projeto de Sistema Web para Gestão de Horas Extras – **2RP**

## 🏢 Empresa Parceira: 2RP

A empresa parceira deste projeto é a **2RP**, especializada em **análise de transações financeiras** e **processamento de dados** com foco na geração de **insights estratégicos** para aprimorar a experiência e a eficiência operacional de seus clientes.

---

## 📌 Problema Identificado

A 2RP identificou a necessidade de um sistema digital para **otimizar a gestão de horas extras**, tanto do ponto de vista operacional quanto gerencial.

Os principais desafios mapeados foram:

### 👤 **Para Usuários (Colaboradores)**

* Registrar horas extras de forma prática e segura.
* Visualizar em tempo real o total de horas acumuladas.

### 👥 **Para Gestores**

* Lançar horas extras de suas equipes.
* Acompanhar os registros em tempo real.
* Gerar relatórios analíticos de produtividade.

### 🛠️ **Para Administradores**

* Gerenciar acessos e permissões.
* Personalizar regras do sistema (como valores de hora extra e horário noturno).
* Validar, aprovar ou reprovar lançamentos de horas.
* Extrair relatórios globais detalhados para auditoria e tomada de decisão.

---

## 💡 Solução Desenvolvida

Com base nas necessidades levantadas, foi desenvolvido um **sistema web responsivo e modular**, com foco em usabilidade, segurança e escalabilidade.

### 🧑‍💼 **Módulo do Administrador**

* Gestão completa de:

  * Usuários.
  * Clientes.
  * Centros de resultado.
* Parametrização do sistema:

  * Definição personalizada de faixas de horário noturno.
  * Estabelecimento dos valores de hora extra (normal e noturna).
* Validação de lançamentos:

  * Aprovação ou reprovação de horas extras enviadas pelos colaboradores.
* Relatórios gerenciais detalhados, exportáveis para auditoria.

### 👨‍💼 **Módulo do Gestor**

* Lançamento manual de horas extras para membros da equipe.
* Acompanhamento em tempo real do desempenho por colaborador.
* Geração de relatórios filtrados por período, colaborador ou centro de resultado.

### 👷 **Módulo do Usuário (Colaborador)**

* Registro individual de horas extras trabalhadas.
* Visualização em tempo real das horas acumuladas no mês.
* Histórico de aprovações e pendências.

---


## GitHub do projeto

- [Repositório no GitHub](https://github.com/api-3sem-pixel-api/api)

---

## 🛠 Tecnologias Utilizadas

### **Java**  
- Utilizado como linguagem principal para desenvolvimento do backend. Sua robustez e portabilidade foram essenciais para a construção de um sistema confiável.  

### **Spring Framework**  
- Forneceu suporte para injeção de dependências, controle transacional e segurança, simplificando o desenvolvimento e garantindo a escalabilidade do sistema.  

### **Maven**  
- Facilitou o gerenciamento de dependências e automação de tarefas, garantindo consistência no ambiente de desenvolvimento.  

### **Vue.js**  
- Framework utilizado para o frontend, permitindo o desenvolvimento de interfaces interativas, modernas e responsivas.  

### **MySQL**  
- Sistema de gerenciamento de banco de dados escolhido por sua confiabilidade e desempenho, garantindo a persistência e integridade dos dados.  

---


## 👤 Contribuições Pessoais

Durante o projeto, atuei como **desenvolvedor full stack**, contribuindo significativamente para a implementação de diversas áreas do sistema. Minhas responsabilidades incluíram tanto o desenvolvimento backend quanto frontend, trabalhando na integração de funcionalidades críticas do sistema.

Além disso, assumi a função de **Scrum Master**, sendo responsável pelo gerenciamento do time, acompanhamento do progresso das sprints e lançamento do gráfico de **burndown**. Também cuidei da **documentação da proposta de solução**, garantindo que todas as etapas do projeto estivessem devidamente registradas e compreendidas pela equipe.

### **Correção no Mapeamento de DTO**

Realizei a implementação do mapeamento de **DTOs (Data Transfer Objects)** para incluir a relação entre o cliente ativo e inativo. O desenvolvimento foi importante para garantir que a comunicação entre as camadas do sistema refletisse corretamente o estado dos clientes no banco de dados.
```java
public record DadosCadastroCliente(String razaoSocialCliente, String cnpjCliente, boolean ativo) {
}
```
Com o DTO e o modelo de dados definidos, criei o modelo Cliente, que facilita a comunicação entre a aplicação e o banco de dados. Esse modelo é responsável por mapear as tabelas correspondentes no banco de dados e garantir que os dados sejam manipulados de forma eficiente.
 

```
@Table(name = "Cliente")
@Entity(name = "Cliente")
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class Cliente {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	@Column(name = "Razao_Social")
	private String razaoSocial;
	private String cnpj;
	private boolean ativo;
	
	@JsonIgnore
	@OneToMany(mappedBy = "cliente")
	private List<LancamentoHoras>lancamento;
	
	public Cliente(Long idCliente) {
		this.id = idCliente;
	}
	
	public Cliente(DadosCadastroCliente dados) {
		this.razaoSocial = dados.razaoSocialCliente();
		this.cnpj = dados.cnpjCliente();
		this.ativo = true;
	}  
}
```

Desenvolvi o controle para exibição das telas de inativação de clientes, incluindo toda a funcionalidade de visualização de clientes . Isso envolveu a comunicação HTTP, criação do layout e a vinculação com o framework VUE. Além de necessitar do uso das diretivas do vue, com o  v-for.

```
<template>
  <Cliente @update-table="loadAllcliente"></Cliente>
  <div class="row">
    <table class="table table-responsive no-wrap-table">
      <thead>
        <tr>
          <th scope="col" class="text-left">Razão Social</th>
          <th scope="col" class="text-left">Cnpj</th>
        
          <th scope="col" class="text-center">Status</th>
          <th scope="col" class="text-center">Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(client, index) in clientes" :key="index">
      
         
          <td>{{ client['razaoSocialCliente'] }}</td>
          <td>{{ client['cnpjCliente'] }}</td>
          <td class="text-center d-flex" style="justify-content: center;"  > <div 
          class="pill approved text-center text-wrap" 
          :class="{
            approved: client['ativo'] == true,
        }" > 
            Ativo 
        </div></td>
          <td class="text-center">
            <button class="btn btn-link"><i class="fa fa-pencil" aria-hidden="true"></i></button>

        <button class="btn btn-link" @click="inativarCliente(client['id'])"><i class="fa fa-trash"  aria-hidden="true" ></i></button>

        
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
```

Desenvolvi uma função para inativar clientes, permitindo a comunicação com a API backend por meio de uma requisição HTTP DELETE, acionada pelo evento de clique no botão do componente. Reproduzindo fielmente o design solicitado pelo nosso UI no Figma e implementando a integração completa entre o backend e o frontend

```
async inativarCliente(clienteId: number) {
  const cliente = this.clientes.find((cliente) => cliente.id === clienteId);
  console.log(cliente);
  if (cliente) {
    if (cliente.ativo) {
      try {
        await http.delete(`/cliente/${clienteId}`);
        cliente.ativo = false;
        alert('Cliente inativado com sucesso');
      } catch (error) {
        alert('Erro ao inativar o cliente. Tente novamente mais tarde.');
      }
    } else {
      alert('O cliente já está inativo');
    }
  } else {
    alert('Cliente não encontrado');
  }
}

  },
});
```

Detalhes

![image](https://github.com/user-attachments/assets/be565bbd-69cf-4a02-9796-eb390e3f27b2)


Foram desenvolvidos os métodos *GET*, *UPDATE* e *POST* para o usuário na interface do front-end, juntamente com a definição de um template para cadastro de usuários.

```


<template>
  <div id="cadastro-user-modal" class="r-modal">
    <div class="r-modal-content">
      <div class="modal-header d-flex align-items-baseline">
        <h4>Cadastro de Usuário</h4>
        <span class="close" @click="close">&times;</span>
      </div>
      <div class="modal-body">
        <div class="row">
          <div class="col-12">
            <div class="form-group">
              <label for="nome">Nome</label>
              <input type="text" class="form-control" id="nome" v-model="nome" />
            </div>
          </div>
        </div>

        <div class="row">
          <div class="col-12">
            <div class="form-group">
              <label for="telefone">Telefone</label>
              <input type="text" class="form-control" id="telefone" v-model="telefone" />
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-12">
            <div class="form-group">
              <label for="email">Email</label>
              <input type="text" class="form-control" id="email" v-model="email" />
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-12">
            <div class="form-group">
              <label for="cpf">CPF</label>
              <input type="text" class="form-control" id="cpf" v-model="cpf" />
            </div>
          </div>
        </div>

        <div class="row">
          <div class="col-12">
            <div class="form-group">
              <label for="funcao">Função</label>
              <select class="form-select" id="funcao" v-model="funcao">
                <option value="Colaborador">Colaborador</option>
                <option value="Administrador">Administrador</option>
                <option value="Gestor">Gestor</option>
              </select>
            </div>
          </div>
        </div>

        <div class="row mt-4">
          <div class="col">
            <button type="button" @click="save" class="btn btn-success">Salvar</button>
            <button type="button" @click="close" class="btn btn-link r-ml-2">Cancelar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
 ```

Detalhes

Listagem de usuarios e demais opções endpoint

![image](https://github.com/user-attachments/assets/90c2920f-a8d1-4db8-b384-e2f325772f8f)

Cadastro de usuario

![image](https://github.com/user-attachments/assets/b45442f3-4090-4f70-b678-93b3b04c6f24)


Criei referente as operações do CRUD, os metodos de update e e read podendo visualizar informações referente ao usuario e atualizar essas mesma informções


 ``` 
  <div class="row">
    <table class="table table-responsive no-wrap-table">
      <thead>
        <tr>
          <th scope="col" class="text-left">Nome</th>
          <th scope="col" class="text-left">Email</th>
          <th scope="col" class="text-left">Telefone</th>
          <th scope="col" class="text-left">CPF</th>
          <th scope="col" class="text-center">Função</th>
          <th scope="col" class="text-center">Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(usuario, index) in usuarios" :key="index">
          <td>{{ usuario['nome'] }}</td>
          <td>{{ usuario['email'] }}</td>
          <td>{{ usuario['telefone'] }}</td>
          <td>{{ usuario['cpf'] }}</td>
          <td>{{ enumUser[usuario['funcao']] }}</td>
          <td class="text-center">
            <button class="btn btn-link" @click="updateUser(usuario.id)">
              <i class="fa fa-pencil" aria-hidden="true"></i>
            </button>
            <button class="btn btn-link" @click="excludedUser(index)">
              <i class="fa fa-trash" aria-hidden="true"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

updateUser(userId: number) {
      this.editUserId = userId;
      var modal = document.getElementById("update-user-modal");
      if (modal) {
        modal.style.display = "block";
      } else {
        console.error("Elemento não encontrado no DOM.");
      }
    },

    async updateUserDetails(updatedUser: any) {
      try {
        await http.put(`/usuario/${this.editUserId}`, updatedUser);

        // Atualize os dados do usuário no array this.usuarios
        const userIndex = this.usuarios.findIndex(u => u.id === this.editUserId);
        if (userIndex !== -1) {
          this.usuarios[userIndex] = updatedUser;
        }

        this.closeUpdateModal(); 
      } catch (error) {
        alert('Erro ao atualizar o usuário. Tente novamente mais tarde.');
      }
    },
    closeUpdateModal() {
      this.editUserId = null; 
      var modal = document.getElementById("update-user-modal");
      if (modal) {
        modal.style.display = "none";
      }
    },


 ``` 

Desenvolvimento da tela de login e ação de entrar no sistema


Implementação da tela de login e do método de autenticação, incluindo a ação de login. A tela não apresentava grande complexidade técnica, o que permitiu concentrar esforços na estilização e na melhoria da experiência do usuário

 ``` 
<template>
  <div class="login-container">
    <div class="login-box-container">
      <div class="login-box">
        <h2>Login</h2>
        <input type="text" placeholder="Usuário" v-model="username" />
        <input type="password" placeholder="Senha" v-model="password" />
        <button @click="login">Entrar</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import  http  from "@/services/http";
import { useAuth } from '@/stores/auth';

export default defineComponent({
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    async login() {
      const auth = useAuth();

      try {
        const user = {
          email: 'emilly94@ramos.com',
          password: '123',
        };

        const { data } = await http.post('/auth', user);
        auth.setToken(data.token);
        auth.setUser(data.user);
        auth.setIsAuth(true);
      } catch (error) {
        console.log(error);
      }
    },
  },
});
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.login-box-container {
  text-align: center;
  background: linear-gradient(to bottom right, #0041d8, #7cbeeb);
}

.login-box {
  background: linear-gradient(to bottom right, #0041d8, #7cbeeb);
  border-radius: 10px;
  padding: 20px;
  margin: 10px 0 40px;

  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  max-width: 500px;
  width: 100%;
}

.login-box h2 {
  margin-bottom: 20px;
}

.login-box input {
  width: 80%;
  max-width: 80%;
  padding: 10px;
  margin: 10px 0 40px;

  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

.login-box button {
  width: 100%;
  max-width: 50%;
  padding: 10px;
  background: #ffffff;
  color: #d3baba;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  border: none;
  border-radius: 5px;
  font-size: 18px;
  cursor: pointer;
  margin-top: 40px;
}
</style>
```


Detalhes 


![image](https://github.com/user-attachments/assets/ce8bc3ca-b563-4fed-a4dd-cd063cfb6332)



### Contribuições como scrum master

Como Scrum Master, fui responsável por organizar o processo de desenvolvimento ágil, gerenciando as sprints e garantindo que a equipe seguisse as práticas ágeis de forma eficiente. Entre minhas responsabilidades, incluí:

Planejamento e organização das sprints, assegurando que as entregas fossem realizadas dentro dos prazos estabelecidos.
Documentação das tarefas no ClickUp, garantindo total visibilidade e acompanhamento do progresso da equipe.
Elaboração do burndown chart das sprints, monitorando o progresso do trabalho e identificando quaisquer impedimentos ou desvios no plano de entrega.

**Hard Skills**

| Tecnologia/Metodologia  | Classificação |
|-------------------------|---------------|
| **SQL**                 | ★★★★★★☆☆☆☆☆  |
| **MySQL**               | ★★★★☆☆☆☆☆☆  |
| **HTML/CSS**            | ★★★★★★★☆☆☆  |
| **Vue**                 | ★★★★★★★☆☆☆  |
| **REST**                | ★★★★★★★☆☆☆  |
| **Scrum**               | ★★★★★★★☆☆☆  |
| **UX/UI Design**        | ★★★★★☆☆☆☆☆  |

**Soft Skills**

| Habilidade             | Classificação |
|------------------------|---------------|
| **Comunicação**        | ★★★★★★☆☆☆☆☆   |
| **Trabalho em Equipe** | ★★★★☆☆☆☆☆☆   |
| **Resolução de Problemas** | ★★★★★★★☆☆☆   |
| **Responsabilidade**   | ★★★★★★☆☆☆☆☆   |





### Justificativa para Hard Skills

| Tecnologia/Metodologia | Justificativa                                                                                               |
|-------------------------|-----------------------------------------------------------------------------------------------------------|
| **SQL**                | Conhecimento intermediário, com habilidade para criar consultas, gerenciar tabelas e manipular dados de maneira eficaz. |
| **MySQL**              | Familiaridade básica no uso desse banco de dados, com experiência em tarefas simples de administração e consultas. |
| **HTML/CSS**           | Boa capacidade de criar layouts estruturados e estilizações consistentes para projetos web.                |
| **Vue**                | Conhecimento intermediário no uso dessa framework, com habilidade para construir componentes e gerenciar estados. |
| **REST**               | Experiência prática na implementação de APIs RESTful, com entendimento sólido de padrões e boas práticas.  |
| **Scrum**              | Aplicação regular dos princípios de Scrum para organização e entrega de projetos, com entendimento de papéis e sprints. |
| **UX/UI Design**       | Habilidade básica em criar interfaces amigáveis e acessíveis, com atenção ao feedback dos usuários.         |

---

### Justificativa para Soft Skills

| Habilidade             | Justificativa                                                                                              |
|------------------------|-----------------------------------------------------------------------------------------------------------|
| **Comunicação**        | Habilidade moderada para transmitir informações e ideias, com potencial para maior clareza e empatia.      |
| **Trabalho em Equipe** | Participação ativa em projetos colaborativos, com necessidade de desenvolver melhor a gestão de conflitos.  |
| **Resolução de Problemas** | Boa capacidade de analisar e solucionar desafios técnicos, buscando soluções criativas e práticas.           |
| **Responsabilidade**   | Consistência no cumprimento de prazos e entrega de tarefas, com espaço para aprimorar a autonomia e proatividade. | 
