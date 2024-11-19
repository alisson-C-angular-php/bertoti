# Projeto de Portal de Avaliação 360° - FATEC

## 🏢 Empresa Parceira
A empresa parceira escolhida para este projeto foi a **FATEC**.

## 📌 Problema
O desafio envolveu a criação de um portal para **avaliação 360 graus**, no qual:
- Cada usuário realiza uma autoavaliação.
- Usuários avaliam os demais membros de sua equipe em **soft skills** preestabelecidas.
- Líderes e POs são avaliados, respectivamente, pelo líder do grupo e pelo **Fake Client**.

## 💡 Solução
A solução desenvolvida proporcionou:
- **Avaliação 360°** dos times.
- Acompanhamento das notas dos usuários em um **dashboard interativo**, permitindo monitorar a evolução a cada sprint.
- Funcionalidades para o administrador gerenciar:
  - Usuários.
  - Composição dos times.
  - Fluxo das sprints.

---

## 🛠 Tecnologias Utilizadas

- **Python**: Backend para criação dos endpoints e implementação dos casos de uso.
- **JavaScript**: Frontend para manipulação de dados e integração com a API.
- **HTML/CSS**: Estilização e estruturação das telas, padrão no desenvolvimento web.
- **FastAPI**: Framework do backend utilizado para criação rápida de APIs e validação automática de dados.

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
