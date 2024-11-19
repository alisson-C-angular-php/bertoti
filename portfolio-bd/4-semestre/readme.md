# Projeto de Sistema de Acompanhamento de Parceiros - Oracle

## 🏢 Empresa Parceira
A empresa parceira escolhida para este projeto foi a **Oracle**.

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
[Clique para ver a lista de hard skills]

## Soft Skills
[Clique para ver a lista de soft skills]
