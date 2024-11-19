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

        // Adicione os dados da lista aprovada ao gráfico de pizza, adicionando a legenda de "Aprovado" e a quantidade aprovada construção para extrair o tipo de usuario talvez necessario?
        int qtdAprovada = extratoHoraDAO.qtdHoraAprovada();
        if (qtdAprovada > 0) {
            pieChartData.add(new PieChart.Data("Aprovado", qtdAprovada));
        }

        // Adicione os dados da lista reprovada ao gráfico de pizza, adicionando a legenda de "Reprovado" e a quantidade reprovada
        int qtdReprovada = extratoHoraDAO.qtdHoraReprovada();
        if (qtdReprovada > 0) {
            pieChartData.add(new PieChart.Data("Reprovado", qtdReprovada));
        }

        dashboard.setData(pieChartData);
    }
```

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
 


# Habilidades Aplicadas no Projeto

| **Categoria**    | **Habilidade**                                     | **Descrição da Aplicação**                                                                          |
|-------------------|---------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Hard Skills**   | **Java**                                          | Desenvolvimento da lógica de negócio, manipulação de dados e criação de eventos no sistema.         |
|                   | **CSS**                                           | Estilização das telas utilizando SceneBuilder para criar layouts responsivos e atrativos.           |
|                   | **MySQL**                                         | Persistência e consulta de dados, garantindo integridade e desempenho do sistema.                   |
|                   | **FXML**                                          | Implementação de rotas e integração de telas no SceneBuilder para navegação fluida no sistema.      |
|                   | **Controle de Acesso**                            | Regras de autenticação e autorização para diferentes perfis de usuário (administradores, gestores). |
|                   | **Relatórios Gráficos**                           | Criação de gráficos em tempo real para acompanhamento de horas trabalhadas.                         |
|                   | **Gestão de Estados**                             | Controle e validação de fluxos, como aprovação/reprovação de horas extras.                          |
|                   | **Boas Práticas de Programação**                  | Modularização do código e implementação de padrões de projeto para maior manutenibilidade.          |
| **Soft Skills**   | **Resolução de Problemas**                        | Análise do problema apresentado pela empresa e criação de uma solução personalizada e funcional.    |
|                   | **Trabalho em Equipe**                            | Colaboração com outros membros da equipe para integração e validação das funcionalidades.           |
|                   | **Comunicação**                                   | Documentação do projeto e apresentação clara das funcionalidades e progresso à equipe parceira.     |
|                   | **Gestão de Tempo**                               | Entrega do projeto dentro do prazo definido, com qualidade e funcionalidades completas.             |
|                   | **Atenção aos Detalhes**                          | Garantia de que as funcionalidades atendem aos requisitos estabelecidos pela empresa parceira.      |
    
