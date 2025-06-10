


### ✅ **Descrição das Atividades do Cliente**

A **Kersys** é uma empresa especializada em soluções inteligentes voltadas ao setor **agroambiental**, com foco na **gestão sustentável de reflorestamentos**. O cliente atua diretamente com produtores, consultores ambientais e órgãos reguladores, oferecendo ferramentas para **monitoramento, planejamento e conformidade ambiental**.
---

## 🔍 **Descrição do Problema Proposto**

A empresa enfrentava desafios no **planejamento estratégico e acompanhamento das áreas reflorestadas**, principalmente no que diz respeito a:

* **Previsão de crescimento das árvores** com base em variáveis ambientais e operacionais;
* **Estimativas de custo** associadas ao processo de reflorestamento;
* **Organização e atualização diária de dados** da plantação por parte dos usuários;
* Necessidade de uma **ferramenta intuitiva, integrada e segura** para tomada de decisão no campo.

---

## 🙋 **Contribuições Pessoais Detalhadas**

Atuei nas áreas de **desenvolvimento front-end e back-end**, com foco nos seguintes módulos:

---

### 🔐 **1. Módulo de Consentimento de Uso de Dados (LGPD)**

#### 🧩 Modelagem de Dados

A estrutura de banco foi organizada conforme o diagrama:

![modelagem-termo](https://github.com/user-attachments/assets/6afba74e-98a1-47ea-8ebb-daf9572c5b3c)

#### 📦 Entidade: `TermoItemAceite`

```java
package br.gov.sp.cps.api.pixel.core.domain.entity;

import jakarta.persistence.*;
import lombok.*;

@Entity
@Table(name = "tb_cad_termo_item_aceite")
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class TermoItemAceite {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long codigo;

    @ManyToOne
    @JoinColumn(name = "termo_aceite_codigo", nullable = false)
    private TermoItemAceiteUsuarioHistorico termoAceiteUsuarioHistorico;

    @ManyToOne
    @JoinColumn(name = "termo_item_codigo", nullable = false)
    private TermoItem termoItem;

    private boolean aceito;
}
```

#### 📦 Entidade: `TermoItemAceiteUsuarioHistorico`

```java
package br.gov.sp.cps.api.pixel.core.domain.entity;

import lombok.*;
import jakarta.persistence.*;
import java.time.LocalDateTime;

@Entity
@Table(name = "tb_cad_termo_item_aceite_usuario_historico")
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class TermoItemAceiteUsuarioHistorico {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long codigo;

    @ManyToOne
    @JoinColumn(name = "usuario_codigo", nullable = false)
    private Usuario usuario;

    @ManyToOne
    @JoinColumn(name = "termo_codigo", nullable = false)
    private Termo termo;

    private LocalDateTime dataAceite;
    private LocalDateTime dataAlteracao;
}
```

#### 🖥️ Interface do Usuário

![UI Screenshot](https://github.com/user-attachments/assets/17ef24fb-b06b-444e-ad0c-438d1a61c896)

#### ✅ Funcionalidades

* Registro de versões e histórico dos termos aceitos;
* Interfaces intuitivas para o usuário aceitar os termos;
* Garantia de conformidade com a **Lei Geral de Proteção de Dados (LGPD)**.

---

### 🧾 **2. Tela de Itens do Termo**

* Área administrativa para cadastrar, editar e excluir itens de consentimento;
* Integração com o módulo LGPD, refletindo as alterações em tempo real.

#### 🔗 Função `enviarDados()`

```typescript
enviarDados() {
  const termo = localStorage.getItem("termo");
  if (termo === "recusou" || this.abriu === false || this.enviando) return;

  if (!this.usuarioNome || !this.email || !this.senha || !this.cpf) {
    this.exibirToast("Por favor, preencha todos os campos obrigatórios.", "danger");
    return;
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(this.email)) {
    this.exibirToast("Por favor, insira um e-mail válido.", "warning");
    return;
  }

  const body = {
    nome: this.usuarioNome,
    nomeUsuario: this.usuarioNome,
    email: this.email,
    senha: this.senha,
    documento: this.cpf,
    funcao: "USUARIO"
  };

  this.enviando = true;

  this.http.post("usuarios", body)
    .then((response: any) => {
      const idUsuario = response.id;

      this.exibirToast("Cadastro realizado com sucesso!", "success");

      const termos = localStorage.getItem("termos");
      if (termos) {
        const termosAceitos = JSON.parse(termos);
        const aceitos = termosAceitos.respostas;
        const codigos = termosAceitos.termoItemCodigo;

        const promessas = codigos.map((codigo: number, i: number) => {
          return this.http.post("historico/aceite", {
            aceito: aceitos[i],
            termoItemCodigo: codigo,
            usuarioCodigo: idUsuario
          });
        });

        Promise.all(promessas)
          .then(() => this.exibirToast("Termos aceitos!", "success"))
          .catch(error => console.error("Erro ao aceitar termos:", error));
      }
    })
    .catch(error => console.error("Erro ao cadastrar usuário:", error))
    .finally(() => this.enviando = false);
}
```

#### 📄 Componente HTML

```html
<ion-header>
  <ion-toolbar>
    <ion-title>Termo de Consentimento LGPD</ion-title>
    <ion-buttons slot="end">
      <ion-button color="medium" (click)="concordar()">Fechar</ion-button>
    </ion-buttons>
  </ion-toolbar>
</ion-header>

<ion-content class="ion-padding" appScrollbar>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Uso de Dados Pessoais</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      <p>
        Conforme a LGPD (Lei nº 13.709/2018), precisamos do seu consentimento para tratar seus dados pessoais.
        Leia os itens abaixo e marque os que concorda.
      </p>
    </ion-card-content>
  </ion-card>

  <ion-list *ngIf="itensObrigatorios?.length || itensOpcionais?.length">
    <ion-list-header color="light">
      <ion-label><strong>Consentimentos Obrigatórios</strong></ion-label>
    </ion-list-header>

    <ion-item *ngFor="let item of itensObrigatorios">
      <ion-checkbox slot="start" [(ngModel)]="respostas[item.codigo]"></ion-checkbox>
      <ion-label>{{ item.descricao }} <strong class="text-danger">*</strong></ion-label>
    </ion-item>

    <ion-list-header *ngIf="itensOpcionais?.length" color="light" class="ion-margin-top">
      <ion-label><strong>Consentimentos Opcionais</strong></ion-label>
    </ion-list-header>

    <ion-item *ngFor="let item of itensOpcionais">
      <ion-checkbox slot="start" [(ngModel)]="respostas[item.codigo]"></ion-checkbox>
      <ion-label>{{ item.descricao }}</ion-label>
    </ion-item>
  </ion-list>

  <ion-note color="medium" class="ion-padding">
    Você pode revogar seu consentimento a qualquer momento nas configurações de privacidade ou contato com o suporte.
  </ion-note>
</ion-content>
```

---

### 🧭 **3. Menu de Navegação**

* Menu lateral responsivo com **Ionic Split Pane**;
* Compatível com dispositivos móveis.

#### 🛣️ Rotas

```typescript
import { Routes } from '@angular/router';

export const routes: Routes = [
  { path: '', redirectTo: 'folder/inbox', pathMatch: 'full' },
  { path: 'folder/:id', loadComponent: () => import('./folder/folder.page').then(m => m.FolderPage) },
  { path: 'dashboard', loadComponent: () => import('./dashboard/dashboard.component').then(m => m.DashboardComponent) },
  { path: 'folder/cadastro', loadComponent: () => import('./cadastro/cadastro.component').then(m => m.CadastroComponent) }
];
```

#### 📁 Componente do Menu

```html
<ion-split-pane id="menu" [ngClass]="isOpenMenu ? 'open' : ''" when="xs" contentId="main">
  <ion-menu contentId="main" style="margin-top: 30px;">
    <ion-label class="ion-align-items-center">
      <h1 class="ion-text-center" style="font-size: 30px;">K</h1>
    </ion-label>

    <ion-content>
      <ng-container *ngFor="let menu of menus;">
        <div class="menu-item" [routerLink]="['/' + menu.link]" routerLinkActive="selected">
          <ion-icon [name]="menu.icon"></ion-icon>
          <ion-label [ngClass]="isOpenMenu ? '' : 'close'">{{ menu.caption }}</ion-label>
        </div>
      </ng-container>
    </ion-content>

    <ion-row class="icon-container">
      <ion-icon name="chevron-forward-outline" *ngIf="!isOpenMenu" (click)="openMenu(true)"></ion-icon>
      <ion-icon name="chevron-back-outline" *ngIf="isOpenMenu" (click)="openMenu(false)"></ion-icon>
    </ion-row>
  </ion-menu>

  <div class="ion-page" id="main">
    <ion-content id="menu-content">
      <ion-router-outlet></ion-router-outlet>
    </ion-content>
  </div>
</ion-split-pane>
```
#### 🖥️ Interfaces


![image](https://github.com/user-attachments/assets/3d5ecf68-51f9-426b-884f-964ab0738ae6)





### 📊 **4. Dashboard de Monitoramento**

* Desenvolvimento de uma tela com **gráficos interativos** que exibem:

  * Crescimento estimado da colheita ao longo de 10 meses;
  * Projeção de custos operacionais;
* Utilização de bibliotecas de visualização de dados integradas ao **Angular**.



Desenvolvido o dashboard

´´´bash
<ion-content appScrollbar>
  <ion-grid  class="plantacao-fundo">
    <ion-row class="ion-justify-content-center">
      <ion-col size="12" size-md="5">
        <ion-card>
          <ion-card-header>
            <ion-title class="ion-text-center">
              <ion-icon name="leaf-outline "></ion-icon> CRESCIMENTO DA COLEITA
            </ion-title>
          </ion-card-header>
          <ion-card-content>
            <p-chart type="line" [data]="growthData" style="max-width: 100%; height: 120px;"></p-chart>
          </ion-card-content>
        </ion-card>
      </ion-col>

      <ion-col size="12" size-md="5">
        <ion-card>
          <ion-card-header>
            <ion-title class="ion-text-center">
              <ion-icon name="cash-outline"></ion-icon> PROJEÇÃO FINANCEIRA
            </ion-title>
          </ion-card-header>
          <ion-card-content>
            <p-chart type="bar" [data]="financeData" style="max-width: 100%; height: 120px;"></p-chart>
          </ion-card-content>
        </ion-card>
      </ion-col>
    </ion-row>

    <ion-row class="ion-justify-content-center">
      <ion-col size="12" size-md="5">
        <ion-card>
          <ion-card-header>
            <ion-title class="ion-text-center">
              <ion-icon name="analytics-outline"></ion-icon> GASTOS COM SOLO
            </ion-title>
          </ion-card-header>
          <ion-card-content>
            <p-chart type="pie" [data]="soilData" style="max-width: 100%; height: 120px;"></p-chart>
          </ion-card-content>
        </ion-card>
      </ion-col>
    </ion-row>
  </ion-grid>
</ion-content>
´´´


#### 🖥️ Interfaces


![image](https://github.com/user-attachments/assets/3b789fca-808e-44c5-b563-6fc41cbeecb8)






---

### 🌱 **5. Tela de Atualização de Plantio**

Interface onde o usuário pode inserir **dados diários da plantação**, como:

* Temperatura ambiente e do solo
* Umidade do ambiente e do solo
* pH do solo
* Índice UV
* Seleção do lote (identificado pelo nome da fazenda)

Os dados são armazenados em bancos de dados **relacional** (`PostgreSQL`) e **não relacional** (`MongoDB`) para permitir cruzamento de informações e análises avançadas.

---

#### 🖼️ **Interface **

<img src="https://github.com/user-attachments/assets/b38d7673-1354-40d8-a3df-7a12b8f56781" alt="Tela de Atualização de Plantio" width="800"/>

---

#### 🧠 **Lógica de Envio de Dados (TypeScript)**

```typescript
async enviarDados() {
  if (
    !this.plantacaoId || this.temperaturaAmbiente === null || this.temperaturaSolo === null ||
    this.umidadeAmbiente === null || this.umidadeSolo === null || this.phSolo === null ||
    this.indiceUV === null
  ) {
    this.exibirToast("Preencha todos os campos obrigatórios!", "danger");
    return;
  }

  const dados = {
    plantacaoId: this.plantacaoId,
    fazendaNome: this.fazendaNome,
    temperaturaAmbiente: this.temperaturaAmbiente,
    temperaturaSolo: this.temperaturaSolo,
    umidadeAmbiente: this.umidadeAmbiente,
    umidadeSolo: this.umidadeSolo,
    phSolo: this.phSolo,
    indiceUV: this.indiceUV,
  };

  this.http.post("atualizacoes", dados).then(() => {
    this.exibirToast("Dados enviados com sucesso!", "success");
    this.router.navigate(['/dashboard']);
  }).catch((error) => {
    const mensagemErro = error?.message || "Erro desconhecido";
    this.exibirToast(`Erro ao enviar os dados! Erro: ${mensagemErro}`, "danger");
  });
}
```

---

#### 🧾 **Formulário HTML (Ionic)**

```html
<ion-content appScrollbar>
  <ion-card>
    <ion-card-header>
      <ion-title class="ion-text-center">
        <ion-icon name="leaf-outline"></ion-icon> FORMULÁRIO DE PLANTAÇÃO
      </ion-title>
    </ion-card-header>

    <ion-card-content>
      <ion-list [inset]="true">
        <ion-grid>

          <!-- Lote -->
          <ion-row>
            <ion-col size="12">
              <ion-title>LOTE</ion-title>
              <ion-item>
                <ion-label position="stacked">SELECIONE UM LOTE *</ion-label>
                <ion-select (ionChange)="onLoteChange($event)" interface="action-sheet" placeholder="Selecione um Lote" required>
                  <ion-select-option *ngFor="let lote of lotes" [value]="lote.id">
                    {{ lote.fazendaNome }}
                  </ion-select-option>
                </ion-select>
              </ion-item>
            </ion-col>
          </ion-row>

          <!-- Temperatura -->
          <ion-row>
            <ion-col size="12">
              <ion-title>TEMPERATURA</ion-title>
            </ion-col>
            <ion-col size="6">
              <ion-item>
                <ion-label position="stacked">TEMPERATURA AMBIENTE (°C) *</ion-label>
                <ion-input type="number" [(ngModel)]="temperaturaAmbiente" required></ion-input>
              </ion-item>
            </ion-col>
            <ion-col size="6">
              <ion-item>
                <ion-label position="stacked">TEMPERATURA DO SOLO (°C) *</ion-label>
                <ion-input type="number" [(ngModel)]="temperaturaSolo" required></ion-input>
              </ion-item>
            </ion-col>
          </ion-row>

          <!-- Umidade -->
          <ion-row>
            <ion-col size="12">
              <ion-title>UMIDADE</ion-title>
            </ion-col>
            <ion-col size="6">
              <ion-item>
                <ion-label position="stacked">UMIDADE AMBIENTE (%) *</ion-label>
                <ion-input type="number" [(ngModel)]="umidadeAmbiente" required></ion-input>
              </ion-item>
            </ion-col>
            <ion-col size="6">
              <ion-item>
                <ion-label position="stacked">UMIDADE DO SOLO (%) *</ion-label>
                <ion-input type="number" [(ngModel)]="umidadeSolo" required></ion-input>
              </ion-item>
            </ion-col>
          </ion-row>

          <!-- Condições do Solo -->
          <ion-row>
            <ion-col size="12">
              <ion-title>CONDIÇÕES DO SOLO</ion-title>
            </ion-col>
            <ion-col size="6">
              <ion-item>
                <ion-label position="stacked">PH DO SOLO *</ion-label>
                <ion-input type="number" step="0.1" [(ngModel)]="phSolo" required></ion-input>
              </ion-item>
            </ion-col>
            <ion-col size="6">
              <ion-item>
                <ion-label position="stacked">ÍNDICE UV *</ion-label>
                <ion-input type="number" [(ngModel)]="indiceUV" required></ion-input>
              </ion-item>
            </ion-col>
          </ion-row>

          <!-- Botão -->
          <ion-row class="ion-justify-content-end">
            <ion-col size="6" size-md="4" class="ion-text-center" style="margin-top: 25px; margin-left: 10px;">
              <ion-button expand="block" type="submit" (click)="enviarDados()">ENVIAR</ion-button>
            </ion-col>
          </ion-row>

        </ion-grid>
      </ion-list>
    </ion-card-content>
  </ion-card>
</ion-content>
```


---

## 💻 **Hard Skills**

| Tecnologia / Metodologia | Nível de Proficiência (★) |
| ------------------------ | ------------------------- |
| **Scrum**                | ★★★★★★☆☆☆☆                |
| **PostgreSQL**           | ★★★★★★★★★★                |
| **Spring Boot (Java)**   | ★★★★★★★★☆☆                |
| **Angular / TypeScript** | ★★★★★★★☆☆☆                |
| **MongoDB**              | ★★★★★★☆☆☆☆                |
| **LGPD (prática)**       | ★★★★★★★☆☆☆                |

---

## 🤝 **Soft Skills**

| Competência                | Nível de Desenvolvimento (★) |
| -------------------------- | ---------------------------- |
| **Comunicação**            | ★★★★★★★★★☆                   |
| **Responsabilidade**       | ★★★★★★☆☆☆☆                   |
| **Organização**            | ★★★★★★★☆☆☆                   |
| **Trabalho em equipe**     | ★★★★★★★★☆☆                   |
| **Resolução de problemas** | ★★★★★★★☆☆☆                   |

---
