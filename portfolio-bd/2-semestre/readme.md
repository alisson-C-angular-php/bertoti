# Projeto de Gestão de Horas Extras - Parceira 2RP  

## 🏢 Empresa Parceira
A empresa parceira escolhida foi a **2RP**.  

---

## 📌 Problema
A necessidade apresentada refere-se à implementação de um sistema para **gerenciar horas extras**.  
As principais funcionalidades solicitadas incluem:  
- Usuários devem registrar suas horas adicionais de trabalho e **acessar informações em tempo real**.  
- Gestores e administradores devem:  
  - **Controlar o acesso** ao sistema.  
  - Extrair **relatórios detalhados** das horas trabalhadas por cada usuário.  
  - Personalizar configurações como:  
    - Definir as **horas iniciais do período noturno**.  
    - Estabelecer os **valores correspondentes às horas extras**.  

---

## 💡 Solução
A solução entregue foi desenvolvida para atender às necessidades específicas de **administradores**, **gestores** e **usuários**:  

### Para Administradores  
- Controle completo (CRUD) de:  
  - Usuários.  
  - Centros de resultado.  
  - Clientes.  
- Parametrização do sistema:  
  - Definição do valor das taxas de trabalho.  
  - Configuração do início/fim das horas noturnas.  
- Extração de relatórios detalhados.  
- Aprovação/reprovação de horas extras lançadas.  

### Para Gestores  
- Lançamento de horas extras.  
- Extração de relatórios relacionados ao gestor ou aos seus funcionários.  
- Acompanhamento em tempo real das horas trabalhadas.  

### Para Usuários  
- Lançamento de horas extras.  
- Acompanhamento detalhado das horas extras acumuladas ao longo do mês.  

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

Como pode ser observado no código acima, a essência da funcionalidade de listagem reprovação de horas extras reside em uma busca no banco de dados, que ocorre assim que um evento de reprovação de horas é disparado.
 


**Hard Skills**

| Tecnologia/Metodologia   | Classificação |
|--------------------------|---------------|
| **SQL**                  | ★★★★★★★★☆☆☆  |
| **MySQL**                | ★★★★★★★☆☆☆  |
| **SceneBuilder/HTML/CSS**| ★★★★★★★★☆☆☆  |
| **Java**                 | ★★★★★★★☆☆☆  |
| **Scrum**                | ★★★★☆☆☆☆☆☆  |

**Soft Skills**

| Habilidade             | Classificação |
|------------------------|---------------|
| **Comunicação**        | ★★★★★★☆☆☆☆☆   |
| **Trabalho em Equipe** | ★★★★★★★☆☆☆   |
| **Resolução de Problemas** | ★★★★★★★★★☆   |
| **Responsabilidade**   | ★★★★★★★☆☆☆   |




### Justificativa para Hard Skills

| Tecnologia/Metodologia     | Justificativa                                                                                               |
|----------------------------|-----------------------------------------------------------------------------------------------------------|
| **SQL**                    | Conhecimento sólido na manipulação de bases de dados, criação de consultas complexas e otimização de queries. Conhecimento esse aplicado na extração de informações para indicadores do processo. |
| **MySQL**                  | Experiência prática na utilização deste SGBD, incluindo configuração, manipulação de tabelas e consultas.    |
| **SceneBuilder/HTML/CSS**  | Boa proficiência em criar interfaces visuais utilizando SceneBuilder, com integração a HTML e CSS para estilização. |
| **Java**                   | Experiência intermediária em desenvolvimento de aplicativos, com foco em projetos orientados a objetos.     |
| **Scrum**                  | Familiaridade básica com a metodologia, participando de sprints e reuniões de planejamento.                 |

---

### Justificativa para Soft Skills

| Habilidade             | Justificativa                                                                                              |
|------------------------|-----------------------------------------------------------------------------------------------------------|
| **Comunicação**        | Habilidade moderada para expressar ideias, com espaço para melhorar a clareza e eficiência na transmissão. Habilidade aplicada no momento de  expressar ideias de como melhorar o sistema e em momentos onde precisave de auxilio para resolver determinados problemas.  |
| **Trabalho em Equipe** | Boa capacidade de colaborar com times, contribuindo positivamente, mas com necessidade de maior prática em conflitos. Habilidade aplicada ao precisar aprender novas habilidades tecnicas e aprender com os membros do grupo |
| **Resolução de Problemas** | Competência notável para identificar e resolver desafios técnicos e lógicos de maneira eficaz.              |
| **Responsabilidade**   | Compromisso consistente com prazos e entrega de qualidade, mas com possibilidade de reforçar a autonomia em tarefas complexas. | 

