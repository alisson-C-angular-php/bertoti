# 📈 Projeto de Sistema de Acompanhamento de Parceiros - **Oracle**

## 🏢 Empresa Parceira: Oracle

A empresa parceira deste projeto é a **Oracle**, uma das líderes globais em tecnologia da informação.

### 🌐 Atuação da Oracle

A **Oracle** é uma multinacional especializada em **tecnologia em nuvem**, oferecendo **infraestrutura de computação, software empresarial e banco de dados** para organizações em todo o mundo. Seu objetivo é ajudar empresas a inovar, operar com mais eficiência e se tornarem mais resilientes e sustentáveis.

O impacto da Oracle vai além do setor corporativo. Suas soluções também apoiam **governos, ONGs e instituições de pesquisa científica e médica**. De pequenas empresas a grandes corporações, milhões de pessoas utilizam as ferramentas da Oracle para:

* Automatizar cadeias de suprimentos;
* Otimizar a gestão de recursos humanos;
* Planejar financeiramente com agilidade;
* Transformar dados em decisões estratégicas.

---

## 📌 Problema Identificado

A Oracle apresentou o desafio de desenvolver um sistema para **monitoramento e gestão de parceiros**, com foco em **capacitação e desempenho regional**.

O sistema precisava contemplar:

* 📍 **Monitoramento da distribuição percentual de parceiros por estado**;
* 🎓 **Acompanhamento da taxa de conclusão dos cursos de capacitação por parceiro**;
* ⏳ **Gestão da validade dos cursos, com alerta para vencimentos próximos**.

---

## 💡 Solução Desenvolvida

Para atender às necessidades da Oracle, foi projetado e implementado um **sistema inteligente e interativo**, com as seguintes funcionalidades:

### 🧑‍💼 Gerenciamento de Usuários e Parceiros

* Cadastro e gerenciamento de **empresas parceiras**, usuários e suas respectivas **trilhas de capacitação**.

### 📊 Dashboard Analítico

* Visualização **em tempo real** da **distribuição geográfica de parceiros**, com mapas e gráficos.
* Indicadores de **taxas de conclusão de cursos** e **nível de engajamento por parceiro**.

### 🔔 Notificações Inteligentes

* Sistema automatizado de **alertas e notificações**, informando parceiros sobre a **proximidade do vencimento dos cursos**.

### 🔐 Controle de Acesso

* Módulo de permissões com diferentes níveis de acesso, garantindo segurança e confidencialidade dos dados.

---

## GitHub do projeto

- [Repositório no GitHub](https://github.com/api-4-sem/api)

---


## 🛠 Tecnologias Utilizadas

### Backend
- **Java**: Linguagem utilizada no backend, amplamente usada em aplicações web e mobile. Escolhida pela robustez e por ser ensinada na FATEC.
- **Spring Boot**: Framework utilizado para:
  - Configuração e estruturação do projeto.
  - Criação de endpoints.
  - Persistência de dados.
  - Segurança da API.

### Frontend
- **TypeScript**: Substituto ao JavaScript, oferecendo:
  - Maior escalabilidade.
  - Melhor manutenção e depuração do código devido à tipagem estática.
- **Vue**: Framework frontend escolhido por sua simplicidade e facilidade de manutenção, com suporte para componentes reutilizáveis.

### Banco de Dados
- **MySQL**: Banco de dados escolhido pela confiabilidade, performance e facilidade de uso, garantindo a persistência e a integridade dos dados do sistema.

---

## 👤 Contribuições Pessoais

### 🔹 Como Product Owner
- **Organização e Criação do Backlog**:
  - Criação e organização de todo o backlog do projeto, incluindo:
    - **User Stories.**
    - Priorização.
    - Alinhamento com o cliente.
  - Estruturação do backlog com **Épicos**, **Features** e organização das **Sprints**.

---

### 🔹 Como Desenvolvedor

#### Endpoint para Criação e Exibição de Empresas
Desenvolvi o endpoint responsável pela criação e exibição da entidade **Empresa**, seguindo os passos abaixo:

1. **Criação do Repository**: 
   Definição de uma interface para mapeamento e carregamento de entidades.


 ```
public interface EmpresaJpaRepository extends JpaRepository<Empresa, Long>, EmpresaRepository {

    @Query(value = """
                    select e.id as id, e.codigo as codigo, e.nome as nome, e.cidade as cidade, e.pais as pais, 
                    e.adminNome as adminNome, e.adminEmail as adminEmail 
                    from Empresa e""")
    List<EmpresaProjection> carregar();
}
 ```


Criação do Projection: Mapeamento dos campos da entidade Empresa para atender à camada de apresentação.


 ```
package br.gov.sp.fatec.apipixel.core.domain.projection;

public interface EmpresaProjection {
    Long getId();
    String getNome();
    String getAdminEmail();
    String getAdminNome();
    String getPais();
    String getCidade();
    Long getCodigo();
}
 ```

Definição da Entidade Empresa: Mapeei a classe Empresa para persistência e utilizei métodos estáticos para facilitar a conversão entre os comandos e a entidade.

```

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Entity
public class Empresa {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "empresa_sequence")
    @SequenceGenerator(name = "empresa_sequence", sequenceName = "empresa_sequence", allocationSize = 1)
    private Long id;
    private Long codigo;
    private String nome;
    private String cidade;
    private String pais;
    private String adminNome;
    private String adminEmail;

    public static Empresa toEntity(CadastrarEmpresaCommand empresaDto){
        Empresa empresa = new Empresa();
        empresa.setCodigo(empresaDto.getCodigo());
        empresa.setNome(empresaDto.getNome());
        empresa.setCidade(empresaDto.getCidade());
        empresa.setPais(empresaDto.getPais());
        empresa.setAdminNome(empresaDto.getAdminNome());
        empresa.setAdminEmail(empresaDto.getAdminEmail());
        return empresa;
    }


    public static Empresa toEntity(CarregarEmpresaUC empresaDto){
        Empresa empresa = new Empresa();
        empresa.getCodigo();
        empresa.getNome();
        empresa.getCidade();
        empresa.getPais();
        empresa.getAdminNome();
        empresa.getAdminEmail();
        return empresa;
    }
 ```

---

## **Contribuições como Scrum Master**

Durante o desenvolvimento de um sistema web para gestão de tarefas acadêmicas, o cliente — um grupo de alunos e professores — buscava uma solução eficiente para organizar e acompanhar atividades, prazos e responsabilidades de forma colaborativa. O desafio principal era garantir a organização das entregas em um curto espaço de tempo, promovendo integração entre os membros e mantendo a qualidade das entregas, mesmo com diferentes níveis de experiência técnica na equipe.

Como **Scrum Master**, atuei como facilitador do processo de desenvolvimento ágil, com foco em garantir que a equipe seguisse os princípios do **Scrum** de forma disciplinada e produtiva. Minhas principais contribuições envolveram:

* **Planejamento e organização das sprints**, definindo claramente os objetivos de cada ciclo de entrega e promovendo reuniões de planejamento e review com o time.
* **Documentação das tarefas no ClickUp**, o que proporcionou total visibilidade para todos os membros da equipe e permitiu que as atividades fossem monitoradas e atualizadas com clareza.
* **Criação e análise de burndown charts**, que ajudaram a identificar gargalos e ajustar o ritmo de trabalho conforme necessário.
* **Mediação de conflitos e facilitação da comunicação entre membros da equipe**, promovendo um ambiente de cooperação e responsabilidade mútua.
* **Aplicação de cerimônias ágeis** (daily meetings, sprint planning e retrospectivas), aumentando a transparência e a capacidade de adaptação diante de mudanças de escopo.

Essas atividades exigiram o uso efetivo de **hard skills**, como o domínio de ferramentas de gestão ágil, conhecimento de **metodologias ágeis (Scrum)**, e capacidade técnica para dialogar com desenvolvedores sobre **APIs REST**, **HTML/CSS**, e **Vue.js**. Paralelamente, foi essencial o uso de **soft skills**, especialmente **comunicação**, **trabalho em equipe**, **resolução de problemas** e **responsabilidade** para conduzir a equipe de forma colaborativa, focada em resultados.

---

## **Hard Skills**

| Tecnologia/Metodologia | Classificação |
| ---------------------- | ------------- |
| **SQL**                | ★★★★★★☆☆☆☆☆   |
| **MySQL**              | ★★★★☆☆☆☆☆☆    |
| **HTML/CSS**           | ★★★★★★★☆☆☆    |
| **Vue**                | ★★★★★★★☆☆☆    |
| **REST**               | ★★★★★★★☆☆☆    |
| **Scrum**              | ★★★★★★★☆☆☆    |
| **UX/UI Design**       | ★★★★★☆☆☆☆☆    |

### Justificativa

| Tecnologia/Metodologia | Justificativa                                                                                             |
| ---------------------- | --------------------------------------------------------------------------------------------------------- |
| **SQL/MySQL**          | Conhecimento funcional na criação de tabelas e execução de queries simples para apoio ao desenvolvimento. |
| **HTML/CSS**           | Desenvolvimento de layouts para interfaces do sistema com foco em responsividade e usabilidade.           |
| **Vue.js**             | Criação e gerenciamento de componentes dinâmicos e reativos da interface do sistema.                      |
| **REST**               | Apoio na implementação e integração de endpoints RESTful no projeto.                                      |
| **Scrum**              | Atuação direta como facilitador no uso da metodologia, aplicando práticas de planejamento e entrega ágil. |
| **UX/UI Design**       | Criação de wireframes e ajustes de interface baseados no feedback dos usuários finais.                    |

---

## **Soft Skills**

| Habilidade                 | Classificação |
| -------------------------- | ------------- |
| **Comunicação**            | ★★★★★★☆☆☆☆☆   |
| **Trabalho em Equipe**     | ★★★★☆☆☆☆☆☆    |
| **Resolução de Problemas** | ★★★★★★★☆☆☆    |
| **Responsabilidade**       | ★★★★★★☆☆☆☆☆   |

### Justificativa

| Habilidade                 | Justificativa                                                                                              |
| -------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Comunicação**            | Facilitou a compreensão entre membros técnicos e não técnicos, essencial para manter todos alinhados.      |
| **Trabalho em Equipe**     | Participação ativa em decisões do grupo, ajudando na integração entre membros com diferentes experiências. |
| **Resolução de Problemas** | Condução de decisões rápidas durante imprevistos nas sprints, como replanejamento de tarefas prioritárias. |
| **Responsabilidade**       | Garantia de que prazos e entregas fossem cumpridos, mantendo o comprometimento com a qualidade.            |

---


