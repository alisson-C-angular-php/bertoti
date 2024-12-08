# Projeto de Dashboard Interativo para Análise de Dados de Recrutamento e Seleção - Pro4tech

## 🏢 Empresa Parceira
A empresa parceira escolhida para este projeto foi a **Pro4tech**.

---

## 📌 Problema
A Pro4tech propôs o desafio de criar um sistema que permitisse aos usuários:
- **Monitorar o desempenho de candidatos em vagas.**
- **Analisarr o perfil de candidatos e sua aderencias a vagas**
- **Acompanhamento, centralização e análise de dados essenciais do processo seletivo.**

---

## 💡 Solução
Desenvolvemos um sistema robusto com as seguintes funcionalidades:
- **Criar um sistema com interface interativa para personalização de gráficos, permitindo selecionar tipo e filtros de dados.**
- **Desenvolver um sistema modular de permissões para definir acessos a conteúdos nos dashboards e outras áreas.** 
- **Desenvolver um sistema de exportação que permita ao usuário baixar os gráficos e dados visualizados diretamente na tela.**.

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
- **Angular**: Framework frontend escolhido por sua simplicidade e facilidade de manutenção, com suporte para componentes reutilizáveis.

### Banco de Dados
- **PostgreSQL**: Banco de dados escolhido pela confiabilidade, performance e facilidade de uso, garantindo a persistência e a integridade dos dados do sistema.

---

## 👤 Contribuições Pessoais

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



Na arquitetura hexagonal foi implementado o endpoint  para post assim acompanhar progresso


´´´
package br.gov.sp.fatec.apipixel.core.domain.command;

import lombok.AllArgsConstructor;
import lombok.Getter;

@Getter
@AllArgsConstructor
public class AcompanharProgressoCommand {

    private Long colaboradorId;
}
´´´





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
| **HTML/CSS**             | Conhecimento básico, suficiente para criar estruturas simples e aplicar estilizações iniciais em projetos web. |
| **Vue**                  | Familiaridade prática com a framework, com capacidade de construir componentes básicos e integrar funcionalidades. |
| **TypeScript**           | Domínio avançado, com habilidade para desenvolver aplicações complexas e aproveitar recursos de tipagem estática. |
| **Scrum**                | Experiência consolidada na aplicação de Scrum para gerenciar projetos, garantir a produtividade e promover a colaboração. |
| **UX/UI Design**         | Forte habilidade em criar interfaces amigáveis e acessíveis, com foco na experiência do usuário e design funcional. |

---

### Justificativa para Soft Skills

| Habilidade             | Justificativa                                                                                              |
|------------------------|-----------------------------------------------------------------------------------------------------------|
| **Comunicação**        | Boa capacidade de expressar ideias e informações, com foco na clareza e adequação ao público-alvo.         |
| **Trabalho em Equipe** | Experiência em colaborar com grupos, com necessidade de desenvolver maior flexibilidade para lidar com diferentes dinâmicas de equipe. |
| **Resolução de Problemas** | Habilidade consistente para analisar situações e propor soluções criativas e eficazes para desafios técnicos. |
| **Responsabilidade**   | Forte senso de compromisso com prazos e objetivos, garantindo a entrega de resultados com qualidade.        | 
