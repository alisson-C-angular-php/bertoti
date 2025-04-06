# Projeto de Dashboard Interativo para Análise de Dados de Recrutamento e Seleção - Pro4tech

## 🏢 Empresa Parceira
A empresa parceira escolhida para este projeto foi a **Pro4tech**.

---

## 📌 Problema
A Pro4tech propôs o desafio de criar um sistema que permitisse aos usuários:
- **Monitorar o desempenho de candidatos em vagas.**
- **Analisar o perfil de candidatos e sua aderencias a vagas**
- **Acompanhamento, centralização e análise de dados essenciais do processo seletivo.**

---

## 💡 Solução
Desenvolvemos um sistema robusto com as seguintes funcionalidades:
- **Criar um sistema com interface interativa para personalização de gráficos, permitindo selecionar tipo e filtros de dados.**
- **Desenvolver um sistema modular de permissões para definir acessos a conteúdos nos dashboards e outras áreas.** 
- **Desenvolver um sistema de exportação que permita ao usuário baixar os gráficos e dados visualizados diretamente na tela.**.

---

## GitHub do projeto

- [Repositório no GitHub](https://github.com/api-5-sem/api-documentation)

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

#### Processamento de excel
Desenvolvi uma função dentro de um componente que é reponsavel por proecessar uma planilha excel de dados e assim enviar esses dados para api que processara os dados do excel, seguindo os passos abaixo:

1. **Criação de botão para enviar arquivo**

   Um tag html foi usada para criar um input do tipo select file onde posso selecionar um arquivo e processalo

```
   <div class="d-flex ms-auto align-items-center">
      <button class="btn btn-light" style="border-radius: 5%;" (click)="triggerFileInput()" aria-label="Importar dados">
        <i class="now-ui-icons files_single-copy-04"></i> Importar
      </button>

      <input type="file" #fileInput style="display: none;" (change)="importDadosProvisionados($event)"
        accept=".xlsx, .xls" />
    </div>

```

Em especifico esse componente visual em Angular utiliza uma div com classes do Bootstrap para alinhar o conteúdo à direita (ms-auto) e centralizar verticalmente os elementos com d-flex e align-items-center. Dentro dessa div, tambem há um botão estilizado com btn btn-light e bordas arredondadas (border-radius: 5%), contendo um ícone da biblioteca Now UI Icons e o texto "Importar". Quando o botão é clicado, ele executa a função triggerFileInput(), que ira  acionar a abertura de um campo de upload de arquivo. Esse campo de upload está logo abaixo, mas está oculto com style="display: none;". É um input do tipo file com a diretiva Angular #fileInput, permitindo que ele seja referenciado no código TypeScrip



2. **Captura do evento click e envio do arquivo**

   Usando uma diretiva que é responsavel por exibir ele primeiro na pagina e é atualizado seu estado quando sofre uma consulta, para isso foi declarado o viewchild

```
      @ViewChild('fileInput') fileInput!: ElementRef;
```

e uma função para capturar esse evento

```
  triggerFileInput() {
    this.fileInput.nativeElement.click();
  }
```



3. **Criação da função**: 
   Definição de um variavel para capturar o arquivo que esta sendo enviado e enviando para a api.


 ```

  importDadosProvisionados(event: any) {
    const file: File = event.target.files[0];

    if (file) {
      this.isLoading = true;

      const formData: FormData = new FormData();
      formData.append('file', file, file.name);

      const headers = new HttpHeaders()
        .set('Authorization', ` ${this.tokenAuth}`)
        .set('enctype', 'multipart/form-data');
  
      this.httpService.post("/api/importacao", formData, { headers })
        .subscribe(
          response => {
            console.log('Arquivo enviado com sucesso', response);
            this.isLoading = false;
          },
          error => {
            console.error('Erro ao enviar arquivo', error);
            this.isLoading = false;
          }
        );
    } else {
      console.log("Nenhum arquivo selecionado.");
    }
  }
```

A função importDadosProvisionados(event: any) é responsável por realizar a importação de um arquivo Excel enviado pelo usuário através de um campo de upload. Quando é selecionado um arquivo, o evento é capturado e o primeiro arquivo da lista é extraído. Em seguida, é criado um objeto FormData, que é usado para enviar dados de formulário contendo arquivos. O arquivo selecionado é adicionado ao FormData com a chave 'file'.

Depois disso, são definidos os cabeçalhos da requisição HTTP, incluindo um cabeçalho de autorização com um token (this.tokenAuth) e o tipo de codificação como multipart/form-data, que é o apropriado para envio de arquivos. O ultimo passo da função  é  fazer uma requisição POST para a URL da nossa api na rota /api/importacao, enviando o FormData com o arquivo e os cabeçalhos configurados. A resposta da requisição é tratada com subscribe: se o envio for bem-sucedido, uma mensagem de sucesso é exibida no console e o carregamento é encerrado; se ocorrer algum erro, uma mensagem de erro é exibida e o carregamento também é encerrado. Caso nenhum arquivo seja selecionado, a função apenas exibe uma mensagem informando que nenhum arquivo foi escolhido.

Detalhes

![image](https://github.com/user-attachments/assets/8089e108-87f6-4492-a72d-b20e7412a223)



4. **Definição de um load**: 
   Definição de um load para que indique o usuario que sua requisição esteja sendo processada.


 ```
.loading {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(255, 255, 255, 0.8);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: red;
  z-index: 9999;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-top: 4px solid red;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
```

Detalhes

![image](https://github.com/user-attachments/assets/c00ce3f9-41fe-4343-ac26-fcbe5688f088)


5. **Testes unitario realizado na função**

 Primeiro testado o envio de requisção que ocorre no endpoint da função.Utilizando o mockfile para simular um dado a ser enviado e a função spyOn para que possa ser simulado da chamada da função real e o mesmo comportamento.

 ```
 it('deve enviar o arquivo corretamente via HTTP', () => {
    const mockFile = new File(['mock content'], 'mockFile.txt', { type: 'text/plain' });
    const mockEvent = { target: { files: [mockFile] } };

    component.importDadosProvisionados(mockEvent);

    const req = httpMock.expectOne('/api/importacao');
    expect(req.request.method).toBe('POST');

    req.flush({ success: true });

    expect(component.isLoading).toBeFalse();
  });
 ```
Basicamente a função spyOn é o principal responsavel pelo meu teste nele eu consigo monitorar métodos durante o teste, que pode ser usado para verificar chamadas, interceptar execuções ou simular retornos.


#### Processamento de dados com filtro para os mesmo que reflitam diretamente os dashboard
Desenvolvido um modal e nesse modal eu posso indicar o tipo de dado que quero que seja exibido no meu dashboard:

 ```
<div class="custom-modal">
  <div class="modal-header">
    <h4 class="modal-title">Gerenciamento de Dashboard</h4>
    <button type="button" class="btn-close" aria-label="Close" (click)="close()"></button>
  </div>

  <div class="modal-body">
    <div class="card">
      <div class="card-body">
        <label for="fatoSelect" class="form-label">Descricao:</label>
        <input [formControl]="form.controls.description" class="form-control mb-3">

        <label for="fatoSelect" class="form-label">Escolha o eixo x:</label>
        <select id="fatoSelect" class="form-control mb-3" [formControl]="form.controls.eixoX.get('nome')">
          <option value="" disabled>Selecione um fato</option>
          <option *ngFor="let fato of fatos" [value]="fato.nome">{{fato.alias}}</option>
        </select>

        <label for="dimensaoSelect" class="form-label mt-3">Escolha um valor para o eixo x:</label>
        <select id="dimensaoSelect" class="form-control mb-3" [formControl]="form.controls.eixoX.get('campo')">
          <option value="" disabled>Selecione um campo</option>
          <option *ngFor="let campo of fatosCampos" [value]="campo">{{ formatarString(campo) }}
          </option>
        </select>

        <label for="campoSelect" *ngIf="tipo != 'card'" class="form-label mt-3">Escolha o eixo y :</label>
        <select id="campoSelect" class="form-control mb-3" *ngIf="tipo != 'card'"
          [formControl]="form.controls.eixoY.get('nome')">
          <option value="" disabled>Selecione um campo</option>
          <option *ngFor="let d of dimensao" [value]="d.nome">{{ d.alias }}</option>
        </select>


        <label for="campoDimensaoSelect" *ngIf="tipo != 'card'" class="form-label mt-3">Escolha um valor para o eixo
          y:</label>
        <select id="campoDimensaoSelect" *ngIf="tipo != 'card'" class="form-control mb-3"
          [formControl]="form.controls.eixoY.get('campo')">
          <option value="" disabled>Selecione um campo</option>
          <option *ngFor="let campo of dimensaoCampos" [value]="campo">{{ formatarString(campo) }}</option>
        </select>


        <label for="campoDimensaoSelect" class="form-label mt-3">Escolha o filtro :</label>
        <select id="campoDimensaoSelect" class="form-control mb-3"
          [formControl]="form.controls.filtros.get('0').get('nome')">
          <option value="" disabled>Selecione um campo</option>

          <option *ngFor="let d of dimensao" [value]="d.nome">{{ d.alias }}</option>
        </select>


        <label for="campoDimensaoSelect" class="form-label mt-3">Escolha um campo/valor para filtrar:</label>
        <select id="campoDimensaoSelect" class="form-control mb-3"
          [formControl]="form.controls.filtros.get('0').get('campo')">
          <option value="" disabled>Selecione um campo</option>
          <option *ngFor="let campo of filtroCampos" [value]="campo">{{ formatarString(campo) }}</option>
        </select>

        <label for="campoDimensaoSelect" class="form-label mt-3">Escolha um comparador:</label>
        <select id="campoDimensaoSelect" class="form-control mb-3"
          [formControl]="form.controls.filtros.get('0').get('comparador')">
          <option value="" disabled>Selecione um campo</option>
          <option value="=">=</option>
          <option value=">=">>=</option>
          <option value="<=">
            <= </option>
          <option value=">">></option>
          <option value="<">
            < </option>
        </select>

        <label for="campoDimensaoSelect" class="form-label mt-3">Escolha um valor do filtro:</label>
        <input id="campoDimensaoSelect" class="form-control mb-3"
          [formControl]="form.controls.filtros.get('0').get('valor')" />

      </div>
    </div>


    <div class="modal-footer">
      <button type="button" class="btn btn-secondary" (click)="close()">Fechar</button>
      <button type="button" class="btn btn-primary" (click)="configure()">Configurar</button>
    </div>
  </div>
</div>
 ```


criação da lógica de como meu componente deve se comporta ao mudar um item no meu combos.Sendos os fatos e dimensões valores preenchidos com base na minha api sempre que uma ação de clique no meu combo for disparada


```
  ngOnInit(): void {
    this.createForm();
    this.getFatos();

    this.form.controls.eixoX.get('nome').valueChanges.subscribe(val => {
      const fato = this.fatos.filter(x => x.nome == val)[0]
      this.fatosCampos = fato.campos[0].split(',')
      this.onFatoChange(val);
    })

    this.form.controls.eixoY.get('nome').valueChanges.subscribe(val => {
      const dimensao = this.dimensao.filter(x => x.nome == val)[0]
      this.dimensaoCampos = dimensao.campos[0].split(',')
    })

    this.form.controls.filtros.get('0').get('nome').valueChanges.subscribe(val => {
      const filtros = this.dimensao.filter(x => x.nome == val)[0]
      this.filtroCampos = filtros.campos[0].split(',')
    })
  }



  createForm() {
    this.form = new FormGroup({
      description: new FormControl('', []),
      eixoX: new FormGroup({
        nome: new FormControl('', []),
        campo: new FormControl('', []),
      }),
      eixoY: new FormGroup({
        nome: new FormControl('', []),
        campo: new FormControl('', []),
      }),
      filtros: new FormArray([new FormGroup({
        nome: new FormControl('', []),
        campo: new FormControl('', []),
        comparador: new FormControl('', []),
        valor: new FormControl('', [])
      })])
    })
  }

  getFatos(): void {
 
    const headers = new HttpHeaders().set('Authorization', `${this.tokenAuth}`);

    this.httpService.get("http://localhost:8080/filtros/fatos", { headers })
      .subscribe({
        next: (responses: any[]) => {
          this.fatos = responses
        }
      });
  }

  onFatoChange(value: string): void {
    
    const headers = new HttpHeaders().set('Authorization', `${this.tokenAuth}`);

    this.httpService.get(`http://localhost:8080/filtros/dimensoes?fato=${value}`, { headers })
      .subscribe({
        next: (response: any[]) => {
          this.dimensao = response;
        }
      });
  }



  configure(): void {
    const form = this.form.value;
    if (!this.form.controls.filtros.get('0').get('nome').value) {
      form.filtros = [];
    }
    sessionStorage.setItem(this.tipo + this.idXGrafico, JSON.stringify(form))
  }

}
```

A função `ngOnInit()` inicializa o formulário e define assinaturas para reagir às mudanças nos campos do formulário, atualizando campos relacionados conforme a seleção do usuário. A função `createForm()` cria a estrutura do formulário reativo com grupos e arrays de controles para captar os dados necessários. A função `getFatos()` faz uma requisição HTTP autenticada para buscar os dados de fatos no backend e armazená-los para uso posterior. Já a função `onFatoChange()` é acionada quando o fato muda, buscando as dimensões correspondentes via HTTP e atualizando os dados disponíveis no formulário.

Detalhes

![image](https://github.com/user-attachments/assets/7d195df6-ff96-4cf3-9dfd-23a33e2da7c4)



2. Processamento dos dados no dashboard com base no meu conteudo que foi filtrado e gravado no meu session storage meu componente dashboard recupera seus dados ao ser inicializado no session storage, como pode se ver na função abaixo


   
```
  createCardRequest(idx: number): DashboardRequest {
    if (idx == 1) {
      const cardOne = JSON.parse(sessionStorage.getItem("card1")) as DashboardRequest;

      if (cardOne) {
        return cardOne
      }
      else {
        return {
          'description': 'Vagas em aberto',
          'eixoX': {
            'nome': 'fato_vaga',
            'campo': 'nr_posicoes_abertas'
          },
          'filtros': []
        }
      }
    }

    if (idx == 2) {
      const cardTwo = JSON.parse(sessionStorage.getItem("card2")) as DashboardRequest;

      if (cardTwo) {
        return cardTwo
      }
      else {
        const now = new Date();
        now.setDate(now.getDate() - 7)

        return {
          'description': 'Entrevistas marcadas',
          'eixoX': {
            'nome': 'fato_entrevista',
            'campo': 'nr_entrevistas'
          },
          'filtros': [
            {
              'nome': 'dim_entrevista',
              'campo': 'dt_entrevista',
              'valor': now.toISOString().split('T')[0],
              'comparador': '>='
            }
          ]
        }
      }
    }

    const cardThree = JSON.parse(sessionStorage.getItem("card3")) as DashboardRequest;
    if (cardThree) {
      return cardThree
    }

    return {
      'description': 'Feedbacks Totais',
      'eixoX': {
        'nome': 'fato_entrevista',
        'campo': 'nr_entrevistas'
      },
      'filtros': []
    }
  }

  createGraphicRequest(idx: number): DashboardRequest {

    if (idx == 1) {
      const grafico1 = JSON.parse(sessionStorage.getItem("grafico1")) as DashboardRequest;
      if (grafico1) {
        return grafico1;
      }
      else {
        return {
          'description': 'Tempo medio do processo',
          "eixoX": {
            "nome": "fato_vaga",
            "campo": "tempo_medio_processo"
          },
          "eixoY": {
            "nome": "dim_vaga",
            "campo": "titulo"
          },
          "filtros": [
            {
              "nome": "dim_periodo",
              "campo": "dt_abertura",
              "comparador": ">=",
              "valor": "2000-09-22"
            }
          ]
        }
      }
    }
    if (idx == 2) {
      const grafico2 = JSON.parse(sessionStorage.getItem("grafico2")) as DashboardRequest;
      if (grafico2) {
        return grafico2;
      }
      else {
        return {
          'description': 'Numero de processos abertos nos ultimos 12 meses ',
          "eixoX": {
            "nome": "fato_vaga",
            "campo": "nr_posicoes_abertas"
          },
          "eixoY": {
            "nome": "dim_vaga",
            "campo": "titulo"
          },
          "filtros": [
            {
              "nome": "dim_periodo",
              "campo": "dt_abertura",
              "comparador": ">=",
              "valor": "2023-09-22"
            }
          ]
        }
      }
    }

    const grafico2 = JSON.parse(sessionStorage.getItem("grafico3")) as DashboardRequest;
    if (grafico2) {
      return grafico2;
    }

    return {
      'description': 'Feedbacks recebidos',
      eixoX: {
        nome: "fato_entrevista",
        campo: "nr_entrevistas"
      },
      eixoY: {
        nome: "dim_feedback",
        campo: "descricao"
      },
      "filtros": [
        {

          "nome": "dim_entrevista",
          "campo": "dt_entrevista",
          "comparador": ">=",
          "valor": "2023-09-22"
        }
      ]
    }
  }
```

#### Tela de login para adentrar no sistema com autenticação via token
Desenvolvido uma tela de login para poder adentrar no sistema:

```
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Login Page</title>
</head>
<body>
  <div class="container">
    <!-- Seção Esquerda -->
    <div class="left-section">
      <div class="logo-container">
        <img src="./assets/img/logo-p4t-navbar-branco.png" alt="Logo" class="logo">
        <h2 class="welcome-title">Bem-vindo ao Nosso Portal</h2>
        <p class="welcome-text">Acesse sua conta para explorar todas as funcionalidades</p>
      </div>
    </div>

    <!-- Seção Direita (Login) -->
    <div class="right-section">
      <div class="login-card">
        <form [formGroup]="loginForm"> 
          <div class="form-group">
            <label for="login" class="form-label">Login</label>
            <input formControlName="login" type="email" id="login"  placeholder="Digite seu login" required />
          </div>
          <div class="form-group">
            <label for="password" class="form-label">Senha</label>
            <input formControlName="password" type="password" id="password"  placeholder="Digite sua senha" required />
          </div>
          <button type="button" class="btn-primary" (click)="onLoginClick()">Entrar</button>
        </form>
        <div class="text-center mt-3">
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

Uma estilização para esse componente de login

```
.card {
    display: flex;
    flex-direction: column; 
    justify-content: center; 
    align-items: center;
    margin: 0 auto; 
    width: 100%; 
    max-width: 400px; 
    padding: 2rem; 
    margin-top: 100px; 
    margin-bottom: 85px; 
    
    border-radius: 12px; 
    border: 2px solid #ffa228; 
    background-color: #f5f5f5; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); 
}

input {
    width: 100%;
    padding: 1.3rem; 
    margin-bottom: 1rem;
    border: 2px solid #ffa228; 
    font-size: 1.1rem; 
}

button {
    background-color: #ffa228; 
    color: white;
    padding: 0.75rem;
    border: none;
    border-radius: 6px;
    font-size: 1rem;
    cursor: pointer;
    width: 100%;
}

button:hover {
    background-color: #0056b3;
}

  @media (max-width: 768px) {
    .container {
      flex-direction: column;
      align-items: center;
      text-align: center;
    }
    
    .image-container {
      margin-bottom: 20px;
    }
    
    .image-container img {
      margin-right: 0; 
    }
  }/* Reset básico */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: Arial, sans-serif;
    background-color: #FF9800;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
  }
  
  /* Container principal */
  .container {
    display: flex;
    width: 100%;
    max-width: 1200px;
    height: 80vh;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }
  
  .left-section {
    flex: 1;
    background-color: #FF9800;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 40px;
    color: #fff;
    text-align: center;
  }
  
  .right-section {
    flex: 1;
    background-color: #f7f7f7;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 40px;
  }
  
  /* Logo e texto de boas-vindas */
  .logo-container {
    max-width: 300px;
  }
  
  .logo {
    max-width: 150px;
    margin-bottom: 20px;
  }
  
  .welcome-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .welcome-text {
    font-size: 16px;
  }
  
  /* Card de login */
  .login-card {
    width: 100%;
    max-width: 400px;
    background-color: #fff;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .form-group {
    margin-bottom: 20px;
  }
  
  .form-label {
    display: block;
    margin-bottom: 8px;
    font-weight: bold;
    color: #333;
  }
  
  .form-control {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  .btn-primary {
    width: 100%;
    padding: 12px;
    background-color: orange ;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;
  }
  
  .btn-primary:hover {
    background-color: #ec463a;
  }
  
  .forgot-password-link {
    color: #007bff;
    font-size: 14px;
    text-decoration: none;
  }
  
  .forgot-password-link:hover {
    text-decoration: underline;
  }
  
  /* Responsividade para dispositivos móveis */
  @media (max-width: 768px) {
    .container {
      flex-direction: column;
      height: auto;
      margin: 20px;
    }
  
    .left-section,
    .right-section {
      width: 100%;
      padding: 20px;
    }
  
    .logo {
      max-width: 120px;
    }
  
    .welcome-title {
      font-size: 20px;
    }
  
    .welcome-text {
      font-size: 14px;
    }
  
    .login-card {
      width: 100%;
      padding: 25px;
    }
  
    .btn-primary {
      font-size: 14px;
      padding: 10px;
    }
  }
```

e a logica do meu componete de login que sera capturar os dados digitados no meu formulario processar o que foi digitado e enviado para logar no sistema

```
  onLoginClick(): void {
    if (this.loginForm.valid == false)  {
      const loginData = this.loginForm.value;
      
      this.http.post<{ token: string; permissaoGrupoProjection: string;}>
            (`${this.apiUrl}/login`, loginData)

      .subscribe({
        next: (response) => {
          localStorage.setItem('authToken', response.token);
          localStorage.setItem('permissions',JSON.stringify(response.permissaoGrupoProjection));
            this.navigate.navigate(['/dashboard']) ;
        },
        error: (error) => {
          console.error('Erro no login:', error);
        }
      });
    } else {
      console.log('Formulário de login inválido');
    }
  }
```

Detalhes

![image](https://github.com/user-attachments/assets/9c89b811-99d6-44f4-a395-e2caddb1de2f)


#### Tela para gerar relatorios
Desenvolvido uma funcionalidade na tela de gerar relatorios, que permite o usuario escolher entre o tipo de relatorio se deseja pdf ou excel:


```
gerarRelatorio() {
     const data = this.request;
   
     const token = 'Bearer ' +localStorage.getItem("authToken");
     const command = data;
   
     this.http.post('http://localhost:8080/relatorio', command, {
       responseType: 'blob',
       observe: 'response',
       headers: {
         Authorization: token 
       }
     }).subscribe(
       (response) => {
         console.log(response)
         const blob = new Blob([response.body], { type: 'application/vnd.ms-excel' });
         const url = window.URL.createObjectURL(blob);
   
         const a = document.createElement('a');
         a.href = url;
         a.download = 'Relatorio.xlsx';
         a.click();
         window.URL.revokeObjectURL(url);
       },
       (error) => {
         console.error('Erro ao gerar o relatório:', error);
       }
     );
   }

```

que basicamente recebe os dados da api ja convertendo no formato excel e realiza o dowload do mesmo


Detalhes

![image](https://github.com/user-attachments/assets/df88863a-317a-4ca4-b197-cfc6ff398b32)



### 🔹 Como DEVOPS

Autei lidando na construção da nossa esteira de automação, o nosso continuos integration. Que é composto por 3 frentes o build, teste, deploy e notificação do sucesso desse processo. Nesse ci foi integrado como nosso processo de desenvolvimento que consistia em adotar um padrao de branch, e validando cada integração de novas funcionalidades até as que as mesma chegassem no ramo principal. Após essa validação que é execultada com teste unitarios, teste de carga e versionamento do nosso banco de dados. Caso nenhuma validação falhe e como mencionado as integrações cheguem ao ramo principal é feito o  build e subido esse conteudo para um container do acr da azure onde realizamos nosso deploy


Action para nosso deploy

```
name: CI/CD Pipeline

on:
  push:
  pull_request:
    branches:
      - main
      - develop
  schedule:
    - cron: '0 18 * * *'

jobs:
  
  build:
    name: Build and Test
    runs-on: ubuntu-latest

    steps:
      # Checkout do código
      - uses: actions/checkout@v3

      # Configuração do Node.js
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20.x'

      # Instalar dependências
      - name: Install dependencies
        run: npm ci
        working-directory: ./api

      # Instalar Angular CLI
      - name: Install Angular CLI
        run: npm install -g @angular/cli@13
        working-directory: ./api

      # Executar testes unitários (somente na branch develop)
      - name: Run unit tests
        if: github.ref == 'refs/heads/develop'
        run: ng test --watch=false --browsers=ChromeHeadless
        working-directory: ./api

  build-and-push-acr:
    name: Build and Push to Azure Container Registry
    runs-on: ubuntu-latest
    if: github.event_name == 'pull_request' && github.base_ref == 'main' # Apenas PR para main

    steps:
    - uses: actions/checkout@master
    
    - uses: Azure/docker-login@v1
      with:
        login-server: angularapp.azurecr.io
        username: ${{ secrets.ACR_USERNAME }}
        password: ${{ secrets.ACR_PASSWORD }}
    
    - run: |
        docker build . -t angularapp.azurecr.io/frontend:${{ github.sha }}
        docker push angularapp.azurecr.io/frontend:${{ github.sha }}
      
    # Set the target AKS cluster.
    - uses: Azure/aks-set-context@v1
      with:
        creds: '${{ secrets.AZURE_CREDENTIALS }}'
        cluster-name: pixelCluster
        resource-group: gr-pixel-containers
      
    - name: Update deployment image
      run: |
        sed -i 's|<IMAGE_PLACEHOLDER>|angularapp.azurecr.io/frontend:${{ github.sha }}|' k8s/deployment.yaml
    - uses: Azure/k8s-deploy@v1
      with:
        manifests: |
          k8s/deployment.yaml
          k8s/service.yaml
        images: |
          angularapp.azurecr.io/frontend:${{ github.sha }}
        imagepullsecrets: |
          k8s-secret-front
        namespace: ingress-basic

  notifyTelegramSuccess:
    runs-on: ubuntu-latest
    needs: [build-and-push-acr, build]
    if: success()
    steps:
      - name: Send Telegram Notification (Success)
        uses: appleboy/telegram-action@v1.0.0
        with:
          to: -4512389085
          token: 7965658930:AAH9K3d8Y2HD73FuMZ7Ys9RSjYfmfErd2zw
          message: |
            ✅ CI/CD Pipeline Status:
            - Evento: ${{ github.event_name }}
            - Branch: ${{ github.ref_name }}
            - Status: Concluído com sucesso!

  notifyTelegramFailure:
    runs-on: ubuntu-latest
    needs: [build-and-push-acr, build]
    if: failure()
    steps:
      - name: Send Telegram Notification (Failure)
        uses: appleboy/telegram-action@v1.0.0
        with:
          to: -4512389085
          token: 7965658930:AAH9K3d8Y2HD73FuMZ7Ys9RSjYfmfErd2zw
          message: |
            ❌ CI/CD Pipeline Failed:
            - Evento: ${{ github.event_name }}
            - Branch: ${{ github.ref_name }}
            - Status: Falha no pipeline. Verifique os logs para mais detalhes!
```



Na primeira etapa como ja comentado,é chamada de build, o workflow instala as dependências do projeto localizado no diretório ./api, configura o ambiente Node.js e instala o Angular CLI. Caso a branch seja develop, ele também executa testes unitários com o comando ng test, garantindo que o código esteja funcionando corretamente. Em seguida, na etapa build-and-push-acr, que roda apenas quando há um pull request direcionado à branch main, o código é empacotado em uma imagem Docker e enviado ao Azure Container Registry (ACR). Após isso, o pipeline conecta-se ao cluster Kubernetes no Azure (AKS) e atualiza a aplicação com a nova imagem, utilizando os arquivos de manifesto deployment.yaml e service.yam


   


---

## Hard Skills

| Tecnologia/Metodologia   | Classificação |
|--------------------------|---------------|
| **HTML/CSS**             | ★★★★☆☆☆☆☆☆☆  |
| **Angular**                  | ★★★★★☆☆☆☆☆  |
| **Github/Actions**           | ★★★★★☆☆☆☆☆  |
| **Typescript**           | ★★★★★★★★★★  |
| **Scrum**                | ★★★★★★★★★★  |
| **UX/UI Design**         | ★★★★★★★★★★  |




## Soft Skills


| Habilidade             | Classificação |
|------------------------|---------------|
| **Comunicação**        | ★★★★★★★☆☆☆☆  |
| **Trabalho em Equipe** | ★★★★★★★★☆☆  |
| **Resolução de Problemas** | ★★★★★★★☆☆☆  |
| **Responsabilidade**   | ★★★★★★★☆☆☆  |



### Justificativa para Hard Skills

| Tecnologia/Metodologia   | Justificativa                                                                                               |
|--------------------------|-----------------------------------------------------------------------------------------------------------|
| **HTML/CSS**             | Conhecimento básico, suficiente para criar estruturas simples e aplicar estilizações iniciais em projetos web. |
| **Angular**                  | Familiaridade prática com a framework, com capacidade de construir componentes básicos e integrar funcionalidades e desenvolver componentes mais personalizados. |
| **TypeScript**           | Domínio avançado, com habilidade para desenvolver aplicações complexas e aproveitar recursos de tipagem estática. |
| **Scrum**                | Experiência consolidada na aplicação de Scrum para gerenciar projetos, garantir a produtividade e promover a colaboração. |
| **UX/UI Design**         | Forte habilidade em criar interfaces amigáveis e acessíveis, com foco na experiência do usuário e design funcional. |

---

### Justificativa para Soft Skills

| Habilidade             | Justificativa                                                                                              |
|------------------------|-----------------------------------------------------------------------------------------------------------|
| **Comunicação**        | Boa capacidade de expressar ideias e informações, com foco na clareza e adequação ao público-alvo. Recendo demandas e processando essas informação via canais de comiunicação.         |
| **Trabalho em Equipe** | Experiência em colaborar com grupos, com necessidade de desenvolver maior flexibilidade para lidar com diferentes dinâmicas de equipe. Podendo lidar com os diferentes requisitos e desafios surgidos durante o projeto e organizando nosso processo de desenvolvimento |
| **Resolução de Problemas** | Habilidade consistente para analisar situações e propor soluções criativas e eficazes para desafios técnicos. Resolvendo nossas demandas de forma concisa e eficiente |
| **Responsabilidade**   | Forte senso de compromisso com prazos e objetivos, garantindo a entrega de resultados com qualidade. Sendo comprometido com a entrega e o foco no resultado.       | 
