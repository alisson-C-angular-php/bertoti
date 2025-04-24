# Projeto de Sistema de Acompanhamento de Parceiros - Oracle

## 🏢 Empresa Parceira
A empresa parceira escolhida para este projeto foi a **Oracle**.


## Atuação da empresa:

Atualmente a oracle é empresa de tecnologia em nuvem que fornece às organizações em todo o mundo infraestrutura de computação e software para ajudá-las a inovar, desbloquear eficiências e se tornar mais eficazes. ento sustentável e se tornar mais resilientes.

O trabalho que fazemos não está apenas transformando o mundo dos negócios - está ajudando a defender os governos e promover a pesquisa científica e médica. De organizações sem fins lucrativos a empresas de todos os tamanhos, milhões de pessoas usam nossas ferramentas para simplificar as cadeias de suprimentos, tornar o RH mais humano, mudar rapidamente para um novo plano financeiro.

---

## 📌 Problema
A Oracle propôs o desafio de criar um sistema que permitisse aos usuários:
- **Monitorar a porcentagem de parceiros por estado.**
- **Acompanhar a taxa de conclusão dos cursos de capacitação de cada parceiro.**
- **Gerenciar a proximidade do vencimento dos cursos de capacitação.**

---

## 💡 Solução
Desenvolvemos um sistema robusto com as seguintes funcionalidades:
- **Gerenciamento de usuários, empresas parceiras e trilhas de ensino.**
- **Acompanhamento em tempo real** do progresso de cada parceiro.
- **Notificações automáticas** baseadas no vencimento dos cursos de capacitação.

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

## Hard Skills

| Tecnologia/Metodologia   | Classificação |
|--------------------------|---------------|
| **HTML/CSS**             | ★☆☆☆☆☆☆☆☆☆☆  |
| **Vue**                  | ★★★☆☆☆☆☆☆☆☆  |
| **Typescript**           | ★★★★★★★★★★  |
| **Scrum**                | ★★★★★★★★★★  |
| **UX/UI Design**         | ★★★★★★★★★★  |




## Soft Skills


| Habilidade             | Classificação |
|------------------------|---------------|
| **Comunicação**        | ★★★★★★★☆☆☆☆  |
| **Trabalho em Equipe** | ★★★★★☆☆☆☆☆  |
| **Resolução de Problemas** | ★★★★★★★☆☆☆  |
| **Responsabilidade**   | ★★★★★★★☆☆☆  |



### Justificativa para Hard Skills

| Tecnologia/Metodologia   | Justificativa                                                                                               |
|--------------------------|-----------------------------------------------------------------------------------------------------------|
| **HTML/CSS**             | Conhecimento básico, suficiente para criar estruturas simples e aplicar estilizações iniciais em projetos web. Construindo estruturas que atendam as necissade de funcionalidades requeridas. |
| **Vue**                  | Familiaridade prática com a framework, com capacidade de construir componentes básicos e integrar funcionalidades entre frontend e backend. Construindo assim sistemas robusto e consistentes. |
| **TypeScript**           | Domínio avançado, com habilidade para desenvolver aplicações complexas e aproveitar recursos de tipagem estática. |
| **Scrum**                | Experiência consolidada na aplicação de Scrum para gerenciar projetos, garantir a produtividade e promover a colaboração. |
| **UX/UI Design**         | Forte habilidade em criar interfaces amigáveis e acessíveis, com foco na experiência do usuário e design funcional. |

---

### Justificativa para Soft Skills

| Habilidade             | Justificativa                                                                                              |
|------------------------|-----------------------------------------------------------------------------------------------------------|
| **Comunicação**        | Boa capacidade de expressar ideias e informações, com foco na clareza e adequação ao público-alvo. Transmiti todas as demandas que foi acordada com o cliente.          |
| **Trabalho em Equipe** | Experiência em colaborar com grupos, com necessidade de desenvolver maior flexibilidade para lidar com diferentes dinâmicas de equipe. Na criação do backlog depois de acertado com o cliente as necessidades do mesmo, trablhei com a equipe transmitido e comunicando as tarefas necessarias para atingirmos essas necessidades. |
| **Resolução de Problemas** | Demonstro habilidade consistente em analisar cenários e propor soluções criativas e eficazes para desafios técnicos. Em situações como a falta de comunicação por parte do cliente, assumo uma postura proativa e estratégica, contribuindo diretamente para o avanço do projeto e garantindo a continuidade das entregas |
| **Responsabilidade**   | Forte senso de compromisso com prazos e objetivos, garantindo a entrega de resultados com qualidade. Utilizei meu senso de compromisso com os objetivos do projeto para garantir que todos os resultados fossem entregues com alta qualidade        | 
