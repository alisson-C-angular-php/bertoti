# 🕒 Projeto de Sistema Web para Gestão de Horas Extras – Parceira **2RP**

## 🏢 Empresa Parceira: 2RP

A empresa parceira escolhida foi a **2RP**, que atua no setor de **análise de transações financeiras** e **inteligência de dados**, com foco na geração de **insights estratégicos** para aprimorar a experiência de seus clientes e impulsionar a tomada de decisão baseada em dados.

---

## 📌 Desafio

A 2RP identificou a necessidade de desenvolver uma aplicação web para a **gestão eficiente das horas extras de seus colaboradores**, com diferentes funcionalidades voltadas aos perfis de **usuários comuns, gestores e administradores**.

### Principais Requisitos:

* Colaboradores devem poder registrar e consultar suas horas extras **em tempo real**.
* Gestores e administradores devem ser capazes de:

  * **Gerenciar acessos** com base em perfis de usuário.
  * **Personalizar parâmetros do sistema**, como:

    * Horário de início do período noturno.
    * Valores atribuídos às horas extras (comum e noturna).
  * **Extrair relatórios gerenciais e analíticos** com filtros por data, usuário, centro de custo, entre outros.

---

## 💡 Solução Desenvolvida

Foi criada uma aplicação web responsiva e segura, com funcionalidades específicas para cada tipo de usuário.

### 🔒 **Administradores**

* Acesso completo ao sistema com funcionalidades de:

  * **CRUD** de usuários, centros de resultado e clientes.
  * Configuração de parâmetros do sistema:

    * Valor da hora extra comum e noturna.
    * Horário de início e término do período noturno.
  * **Aprovação e reprovação** de lançamentos realizados por colaboradores.
  * Geração de **relatórios gerenciais detalhados**, com exportação em múltiplos formatos.

### 👨‍💼 **Gestores**

* Lançamento de horas extras para membros de sua equipe.
* Visualização e análise em tempo real das horas lançadas por colaboradores sob sua gestão.
* Acesso a relatórios específicos com filtros personalizados.

### 👷 **Usuários (Colaboradores)**

* Lançamento individual das horas extras realizadas.
* Acompanhamento diário e mensal das horas extras acumuladas.
* Visualização de status dos lançamentos (pendente, aprovado ou reprovado).

---

## ⚙️ Tecnologias Utilizadas

* **Frontend:** Angular + TypeScript
* **Backend:** Java com Spring Boot
* **Banco de Dados:** PostgreSQL
* **Controle de Versão:** Git e GitHub
* **Metodologia:** Desenvolvimento ágil com foco em entregas modulares e testes contínuos

---

## 👨‍💻 Contribuições Pessoais

Durante o projeto, atuei diretamente nas seguintes frentes:

* Desenvolvimento e integração dos módulos de autenticação, lançamento e validação de horas.
* Implementação das regras de negócio para cálculo das horas extras com base em faixas horárias.
* Construção dos componentes de relatório e filtros personalizados por perfil.
* Integração completa entre frontend e backend via API REST.
* Versionamento de código e organização da estrutura do repositório.

---

## 🧠 Habilidades Desenvolvidas

### Técnicas (Hard Skills)

* Programação com **Java (Spring Boot)** e **Angular**.
* Consumo e criação de **APIs RESTful**.
* Modelagem e manipulação de dados em **PostgreSQL**.
* Arquitetura MVC, controle de permissões e autenticação JWT.
* Versionamento e colaboração com **Git/GitHub**.

### Interpessoais (Soft Skills)

* Colaboração em equipe multidisciplinar.
* Adaptação a requisitos dinâmicos.
* Comunicação efetiva e organização no trabalho em equipe.
* Resolução ágil de problemas técnicos.

---

## GitHub do Projeto  
- [Repositório no GitHub](https://github.com/api-2-sem/api)  

---

## 🛠 Tecnologias Utilizadas

### **Java**  
- **Linguagem principal** do projeto.  
- Utilizada para manipulação de dados e criação de eventos atrelados à exibição de informações.  

### **CSS**  
- Utilizado para estilização das telas.  
- Escolhido pela integração com o **SceneBuilder**, facilitando a criação de layouts atrativos.  

### **MySQL**  
- Escolhido pela sua confiabilidade, desempenho e facilidade de uso.  
- Responsável por garantir a **persistência** e **integridade dos dados** do sistema.  

---

## 👤 Contribuições Pessoais


Nesse projeto atuei como desenvolvedor. Como desenvolvedor, minhas contribuições foram:

Detalhes 

```
public class Login{
	private String email;
	private String password;
	
	public Login(String email, String password) {
		this.email = email;
		this.password = password;
	}
	
	public boolean auth(String email,String password) {
		Login login = new Login(email, password);
		return this.email.equals(email) && this.password.equals(password);
	}
}
```

A classe Login possui dois atributos privados: email e password, que armazenam respectivamente o e-mail e a senha do usuário. Ao instanciar a classe através do construtor Login(String email, String password), esses dois atributos são inicializados com os valores fornecidos.

O método auth(String email, String password) serve para verificar se os dados fornecidos coincidem com os armazenados. Ele cria um novo objeto Login com os parâmetros recebidos (embora essa instância não seja realmente usada) e retorna true apenas se o e-mail e a senha passados como argumento forem exatamente iguais aos armazenados no objeto original (this.email e this.password). Caso contrário, retorna false


Fui encarregado de criar a tela de login no SceneBuilder, utilizando para isso CSS e algumas imagens padrões da empresa parceira. Nessa mesma tela foi implementado regras de acesso ao sistema.

Detalhes

![image](https://github.com/user-attachments/assets/08436240-9df9-4d58-b94c-ccac1a7b34f4)

Como email e senha

Desenvolvimento de feedbacks alertando o usuario sobre sucesso de operacao 

```
public class MensagemRetorno {	
	public MensagemRetorno() {
		super();
	}

	public static void sucessoCadastro() {
		sucesso("Cadastro efetuado com sucesso");
	}

	public static void sucesso(String message) {
		Alert alert = new Alert(AlertType.INFORMATION);
		alert.setContentText(message);
		alert.show();
	}
	
	public static void erroCadastro() {
		erro("Não foi possível efetuar o cadastro");
	}

	public static void erro(String message) {
		Alert alert = new Alert(AlertType.ERROR);
		alert.setContentText(message);
		alert.show();
	}
}
```

A classe MensagemRetorno tem como principal objetivo centralizar e padronizar a exibição de mensagens para o usuário, especialmente em aplicações com interface gráfica desenvolvidas em JavaFX. Por meio de métodos estáticos, ela permite mostrar mensagens de sucesso ou erro utilizando caixas de diálogo (Alert), o que contribui para uma melhor experiência do usuário


Estabeleciomento de rota para tela de cadastro de usuario 

 ```
 @FXML
    void irControleUsuario(MouseEvent event) {
        changeScene("/view/CadastroUsuario.fxml");
    }
 ```

Detalhes 

![image](https://github.com/user-attachments/assets/963fb8b8-b836-4a4f-8ee0-13aecba109c9)


Uma maneira de estabelecer navegacao no sistema

Foi desenvolvido um dashboard 


```

    @FXML
    protected void initialize() {
        ExtratoHoraDAO extratoHoraDAO;


        ObservableList<PieChart.Data> pieChartData = FXCollections.observableArrayList();

        int qtdAprovada = extratoHoraDAO.qtdHoraAprovada();
        if (qtdAprovada > 0) {
            pieChartData.add(new PieChart.Data("Aprovado", qtdAprovada));
        }

        int qtdReprovada = extratoHoraDAO.qtdHoraReprovada();
        if (qtdReprovada > 0) {
            pieChartData.add(new PieChart.Data("Reprovado", qtdReprovada));
        }

        dashboard.setData(pieChartData);
    }
```

Se houver algum aprovado ele entra na seção de aprovado caso nao entra no reporvado e 

Detalhes


![image](https://github.com/user-attachments/assets/7cb06e1a-8040-4770-953e-7c788d2f10e0)

Como podem ver o colaborador pode contabalizar as horas que foi aprovada e reprovada no sistema

Desenvolvimento de regra para pegar horas reprovadas no sistema

```
 //select para pegar horas reaprovada 
    public int qtdHoraReprovada() {
    	try {
    		String sql = "FROM extrato_hora SELECT Id_Etapa_Extrato";
    		executarQuery(sql);
    		return executarQuery(sql);
    	}catch(Exception e) {
    		e.addSuppressed(e);
    	}
}
```


## 🛠 Hard Skills

| Tecnologia / Metodologia      | Nível de Proficiência      |
| ----------------------------- | -------------------------- |
| **SQL**                       | ★★★★★★★★☆☆☆ (Avançado)     |
| **MySQL**                     | ★★★★★★★☆☆☆ (Intermediário) |
| **SceneBuilder / HTML / CSS** | ★★★★★★★★☆☆☆ (Avançado)     |
| **Java**                      | ★★★★★★★☆☆☆ (Intermediário) |
| **Scrum**                     | ★★★★☆☆☆☆☆☆ (Básico)        |

### 🔎 Justificativa das Hard Skills

| Tecnologia / Metodologia      | Justificativa                                                                                                 |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **SQL**                       | Experiência sólida em manipulação de dados, criação de views e queries complexas para geração de indicadores. |
| **MySQL**                     | Aplicação prática do SGBD no projeto, com foco em performance, normalização e consistência dos dados.         |
| **SceneBuilder / HTML / CSS** | Criação de interfaces funcionais e bem estruturadas, com atenção à experiência do usuário e responsividade.   |
| **Java**                      | Desenvolvimento das funcionalidades principais do backend utilizando orientação a objetos.                    |
| **Scrum**                     | Participação em reuniões de planejamento e revisão de sprint, com uso de artefatos como backlog e daily.      |

---

## 💡 Soft Skills

| Habilidade                 | Nível de Desenvolvimento |
| -------------------------- | ------------------------ |
| **Comunicação**            | ★★★★★★☆☆☆☆ (Moderado)    |
| **Trabalho em Equipe**     | ★★★★★★★☆☆☆ (Bom)         |
| **Resolução de Problemas** | ★★★★★★★★★☆ (Muito Bom)   |
| **Responsabilidade**       | ★★★★★★★☆☆☆ (Bom)         |

### 🔎 Justificativa das Soft Skills

| Habilidade                 | Justificativa                                                                                                                        |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Comunicação**            | Atuei de forma clara ao expor ideias e dúvidas, principalmente ao sugerir melhorias e buscar ajuda para resolver problemas técnicos. |
| **Trabalho em Equipe**     | Contribuí ativamente com o grupo, especialmente em momentos de aprendizado coletivo e colaboração técnica.                           |
| **Resolução de Problemas** | Demonstrei eficiência na identificação e resolução de problemas técnicos, especialmente em SQL e integração com o backend.           |
| **Responsabilidade**       | Entreguei todas as demandas sob minha responsabilidade dentro do prazo, com qualidade e comprometimento.                             |

---
