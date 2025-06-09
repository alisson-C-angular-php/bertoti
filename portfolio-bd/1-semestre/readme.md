# 🎯 Projeto: Portal de Avaliação 360° – FATEC

## 🏢 Empresa Parceira: FATEC

A **Faculdade de Tecnologia (FATEC)** foi a instituição parceira deste projeto, cuja proposta visava aprimorar o processo de avaliação comportamental e colaborativa entre membros de times de desenvolvimento ágil.

---

## 📌 Desafio

O desafio consistiu na criação de um **portal de avaliação 360 graus**, com foco no desenvolvimento e acompanhamento de **soft skills** entre os participantes de projetos ágeis. As regras estabelecidas incluíram:

* Cada usuário deve realizar uma **autoavaliação**.
* Os usuários também avaliam **todos os demais membros de sua equipe**.
* Avaliações são feitas com base em critérios predefinidos de **habilidades interpessoais (soft skills)**.
* Líderes de equipe são avaliados pelo líder do grupo, enquanto os **Product Owners (POs)** são avaliados pelo **Fake Client** (cliente fictício designado).

---

## 💡 Solução Desenvolvida

Foi implementado um **portal web completo** para gerenciar e centralizar o processo de avaliação contínua durante os ciclos de sprint.

### Principais Funcionalidades:

* Avaliação 360° entre membros da equipe.
* Painel interativo com **dashboard de desempenho** por sprint.
* Acompanhamento da **evolução dos resultados** ao longo do tempo.
* Funcionalidades administrativas para:

  * Cadastro e gestão de usuários.
  * Configuração e manutenção das equipes de trabalho.
  * Definição do cronograma de sprints e liberação dos ciclos de avaliação.

---

## ⚙️ Tecnologias Utilizadas

* **Backend:**

  * **Python** com **FastAPI** – Criação de endpoints RESTful, rotas protegidas, validação de dados com Pydantic e estruturação de regras de negócio.

* **Frontend:**

  * **JavaScript** – Manipulação do DOM e consumo da API.
  * **HTML/CSS** – Estruturação visual e estilização responsiva das telas.

* **Integração:**

  * Comunicação assíncrona entre frontend e backend utilizando requisições HTTP via **fetch API**.

---


## 👤 Contribuições Pessoais


### Como Desenvolvedor
1. **Crud de perfil de usuario**:
   - Criado todas as operações em relação ao crud do perfil de usuario.
   - Desenvolvida a lógica de abstração para realizar operações de **CRUD** no "banco" de dados.


```
class profile_repository(object):
    _apiContext: ApiContext = ApiContext()
    def __init__(self) -> None:
        pass
    def get(self):
        return self._apiContext.user_table.get_all()
    def busca_id_profile(self,id):
        return self._apiContext.profile_table.get(id)
    def post_profile(self, objectPost):
        self._apiContext.profile_table.begin_transaction()
        self._apiContext.profile_table.insert(objectPost)
        self._apiContext.profile_table.commit()
    def put_profile(self, objectPut):
        self._apiContext.profile_table.begin_transaction()
        self._apiContext.profile_table.commit()
        self._apiContext.user_table.begin_transaction()
        self._apiContext.user_table.update(objectPut)
        self._apiContext.user_table.commit()
    def delete_id_usuario(self, id:int):
        self._apiContext.user_table.begin_transaction()
        self._apiContext.user_table.delete(id)
        self._apiContext.user_table.commit()
```

A classe profile_repository foi construída para encapsular as operações de leitura, escrita, atualização e exclusão de perfis e usuários em um sistema

2. **Implementação de validação para verificar a que turma um usuario pertencia**:
   - Desenvolvimento completo do endpoint e comunicação com banco:


 ```
 def create(self, model: grupo_model):

        grupoBd = self._modelToBd(model)
        times_em_grupo = self._teamsRepository.findTeamByGroup(grupoBd.id)
        grupo = self._grupo_repository.busca_id_grupo(grupoBd.id)
        grupo_id=self._grupo_repository.get(grupo.get('id'))


        for time in times_em_grupo:
            if time == grupo_id:
                raise Exception("Este time ja esta associado a este grupo");

        item = self._grupo_repository.post_grupo(grupoBd)
        model.id = item.id;
        self.updateTeam(model);
 ```

Percorrido o grupo eu consigo validar se ja pertence um time naquele grupo que correpondam ao usuario, garantindo que não haja duplicidade de times dentro do grupo
 

3. **Implementação da listagem de usuario**:
   - Desenvolvimento de endpoint para listagem de usuario.

   Detalhes

```
class usuario_services(object):
    _user_repository:user_repository = user_repository()
    def __init__(self):
        pass;
    def buscar_usuario(self):
        return self._user_repository.get()

```
   
5. **Implementação de roteamento**:
   - Desenvolvimento de rotas para endpoint.


```
   from fastapi import APIRouter
from ..controllers import usuario_controler, test_controller, autenticacao_controller

router = APIRouter()
router.include_router(test_controller.router)
router.include_router(autenticacao_controller.router)
router.include_router(usuario_controler.router)

```

---

## 🛠 Hard Skills

| Tecnologia / Metodologia | Nível de Proficiência             |
| ------------------------ | --------------------------------- |
| **Python**               | ★★★★★★★★★★ (Avançado)             |
| **HTML/CSS**             | ★★★☆☆☆☆☆☆☆ (Básico-Intermediário) |
| **JavaScript**           | ★★★☆☆☆☆☆☆☆ (Básico-Intermediário) |
| **FastAPI**              | ★★★★★★★★★★ (Avançado)             |
| **Scrum**                | ★★★★★★★★★★ (Avançado)             |

### Justificativas para Hard Skills

| Tecnologia / Metodologia | Justificativa                                                                                                  |
| ------------------------ | -------------------------------------------------------------------------------------------------------------- |
| **Python**               | Proficiência avançada no desenvolvimento de aplicações backend, automação de processos e análise de dados.     |
| **HTML/CSS**             | Conhecimento sólido em estruturação e estilização de páginas, com foco em responsividade e usabilidade básica. |
| **JavaScript**           | Experiência inicial, suficiente para manipulação do DOM e integração com APIs REST no frontend.                |
| **FastAPI**              | Expertise no desenvolvimento de APIs RESTful escaláveis e performáticas, com validação robusta de dados.       |
| **Scrum**                | Vivência prática em gerenciamento ágil de projetos, facilitando entregas incrementais e trabalho colaborativo. |

---

## 💡 Soft Skills

| Habilidade                 | Nível de Desenvolvimento |
| -------------------------- | ------------------------ |
| **Comunicação**            | ★★★★★★★★★★ (Excelente)   |
| **Trabalho em Equipe**     | ★★★★★★★★★☆ (Muito Bom)   |
| **Resolução de Problemas** | ★★★★★★★★★★ (Excelente)   |
| **Responsabilidade**       | ★★★★★★★★★★ (Excelente)   |

### Justificativas para Soft Skills

| Habilidade                 | Justificativa                                                                                                                        |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Comunicação**            | Capacidade notável para expressar ideias de forma clara e objetiva, facilitando o entendimento em ambientes técnicos e não técnicos. |
| **Trabalho em Equipe**     | Experiência sólida em colaboração multidisciplinar, promovendo um ambiente de trabalho harmonioso e produtivo.                       |
| **Resolução de Problemas** | Aptidão para identificar desafios complexos e implementar soluções inovadoras e eficazes.                                            |
| **Responsabilidade**       | Comprometimento consistente com prazos e qualidade, garantindo entregas confiáveis e alinhadas às expectativas.                      |

---

