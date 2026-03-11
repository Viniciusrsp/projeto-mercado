# projeto-mercado

# Documento de Escopo do Projeto

## 1. Identificação do Projeto

**Nome do projeto:** Controle de Estoque para Mercado  

**Grupo (nomes):**  
- Vinicius Ribeiro de Souza Pinto  
- André Luiz Augusto  
- Luiz Gabriel Santos de Sá da Silva  
- Weder Pereira dos Santos  
- Murilo Augusto Seripieri
- Igor Alexandre Paula Alves
- Erick Moreira do Nascimento
- Nicole Lucio Martins
- Mateus Pedrosa Saudanha

**Versão/Data:** 1.0 | 04/03/2026

---

# 2. Visão Geral da Empresa

O **Mercado Bom Preço** é um mercado de bairro de pequeno porte, em funcionamento há 5 anos, localizado em região residencial. Atualmente opera com **3 funcionários** (dona, um repositor e um caixa) e atende cerca de **80 clientes por dia**.

A operação diária funciona da seguinte forma:

- As compras dos clientes são registradas em **cupom fiscal (obrigatório)**.
- O **controle de estoque é feito manualmente em planilhas Excel**.
- A dona atualiza as planilhas ao final do dia, quando confere as vendas e tenta estimar o que precisa ser reposto.
- Não há cadastro formal de clientes, apenas **vendas à vista**.

A cultura organizacional é **familiar e informal**, com processos simples mas pouco padronizados.

A dona toma a maioria das decisões baseada na experiência, mas com a expansão (pretende abrir **uma segunda unidade em 1 ano**), percebeu que precisa de mais controle de estoque.

**Valores da empresa:**

- Baixo custo  
- Simplicidade (funcionários têm pouca familiaridade com tecnologia)  
- Agilidade no dia a dia  

---

# 3. Problema Atual (Dor) e Consequências

## Como funciona hoje

- O estoque é controlado por **planilhas Excel** que a dona atualiza manualmente ao final do expediente.
- Os produtos são anotados em uma **lista de compras** quando alguém percebe que está acabando.
- Não existe **alerta automático de estoque baixo**.
- Quando chega mercadoria nova, a dona precisa conferir **nota fiscal** e atualizar a planilha.
- Às vezes a atualização **é esquecida ou feita com erro**.

## Impactos do problema

- **Perda de vendas por falta de estoque**  
  - Clientes procuram um produto e não encontram, indo ao concorrente.

- **Erros de contagem**  
  - A dona gasta cerca de **2 horas por dia** atualizando planilhas e mesmo assim os números não fecham.

- **Excesso de compra de produtos**  
  - Compra duplicada ou em quantidade maior que o necessário.

- **Dificuldade de expansão**  
  - Com uma segunda unidade, seria difícil gerenciar **planilhas separadas**.

---

# 4. Objetivo da Solução

## Objetivo Principal

Criar um **sistema desktop simples para controle de estoque**, eliminando as planilhas manuais e evitando falta de mercadoria.

## Benefícios Esperados

- Reduzir o tempo gasto com atualização de estoque (**de 2 horas/dia para 15 minutos**)
- Saber exatamente **o que tem no estoque a qualquer momento**
- Evitar falta de produtos mais vendidos com **alertas de estoque baixo**
- Facilitar a **conferência de mercadorias recebidas**

---

# 5. Stakeholders e Perfis de Usuário

## Dona / Administradora

**Responsabilidades**

- Gerenciar o negócio
- Cadastrar produtos
- Realizar compras
- Conferir estoque
- Consultar relatórios

**Objetivos**

- Ter visão completa do estoque
- Saber o que precisa comprar
- Identificar produtos parados

---

## Funcionário

**Responsabilidades**

- Registrar entrada de mercadorias
- Consultar estoque
- Avisar quando produtos estão acabando

**Necessidades**

- Interface simples
- Busca rápida de produtos
- Sistema fácil de usar

---

# 6. Escopo do Sistema

## Dentro do Escopo (IN)

- Cadastro de produtos
  - nome
  - código de barras
  - categoria
  - preço de custo
  - preço de venda
  - estoque mínimo
  - quantidade atual

- Categorias de produtos  
  - Ex: bebidas, limpeza, mercearia, hortifruti

- Entrada de mercadoria  
  - Registrar chegada de novos produtos

- Saída / baixa de estoque  
  - Diminuir quantidade por venda, perda ou vencimento

- Consulta de estoque  
  - Listar produtos
  - Buscar por nome
  - Filtrar por categoria

- Relatório de estoque baixo

---

## Fora do Escopo (OUT)

- Cadastro de clientes
- Integração com emissão de nota fiscal
- Controle financeiro (contas a pagar/receber)
- Acesso via internet ou aplicativo
- Sistema será **apenas desktop local**

---

# 7. Requisitos Funcionais (RF)

| Código | Requisito |
|------|------|
| RF01 | Cadastrar categoria |
| RF02 | Cadastrar produto |
| RF03 | Consultar produtos |
| RF04 | Registrar entrada de mercadoria |
| RF05 | Registrar saída / baixa de estoque |
| RF06 | Visualizar estoque atual |
| RF07 | Alertar estoque baixo |
| RF08 | Gerar relatório mensal |

---

# 8. Regras de Negócio (RN)

| Código | Regra |
|------|------|
| RN01 | Não pode existir dois produtos com o mesmo código de barras |
| RN02 | Preço de venda deve ser maior que o preço de custo |
| RN03 | Categoria deve existir antes de cadastrar produto |
| RN04 | Estoque mínimo deve ser maior que zero |
| RN05 | Toda movimentação registra data e usuário |

---

# 9. Requisitos Não Funcionais (RNF)

- **Interface simples e intuitiva**  
  Fácil uso por pessoas com pouca experiência em computador

- **Persistência local**  
  Dados armazenados em:
  - JSON
  - CSV
  - ou SQLite

- **Tempo de resposta**  
  Consultas devem retornar em **menos de 2 segundos**

- **Disponibilidade**  
  Sistema funciona **sem internet**

- **Manutenibilidade**  
  Código organizado em **camadas (interface, regras e dados)**

---

# 10. Entidades Principais (Classes de Domínio)

## Categoria
- id
- nome

## Produto
- id
- nome
- codigoBarras
- precoCusto
- precoVenda
- estoqueMinimo
- quantidadeAtual
- categoria

## Movimentacao
- id
- tipo (ENTRADA / SAIDA)
- quantidade
- dataHora
- motivo
- produto
- usuario

## Usuario
- id
- nome
- login
- senha
- perfil (DONA / FUNCIONARIO)

## Relatorio
Entidade lógica (não persistida).

---

# 11. Casos de Uso

| Código | Caso de Uso | Ator | Descrição |
|------|------|------|------|
| UC01 | Cadastrar categoria | Dona | Criar categoria para organizar produtos |
| UC02 | Cadastrar produto | Dona | Registrar novo produto |
| UC03 | Consultar estoque | Dona / Funcionário | Buscar produtos e quantidades |
| UC04 | Registrar entrada | Dona / Funcionário | Adicionar quantidade ao estoque |
| UC05 | Registrar saída | Dona / Funcionário | Reduzir estoque por venda ou perda |
| UC06 | Visualizar alertas | Dona | Ver produtos com estoque baixo |

---

# 12. Cenários de Uso

## Cenário 1 — Fluxo principal (Chegada de mercadoria)

1. Funcionário recebe entrega com **20 unidades de arroz**
2. Abre o sistema
3. Acessa **Registrar Entrada**
4. Busca produto **Arroz Tipo 1**
5. Digita quantidade **20**
6. Confirma operação
7. Sistema atualiza estoque **35 → 55**
8. Sistema registra **data, hora e usuário**

---

## Cenário 2 — Exceção (Saída maior que estoque)

1. Cliente compra **10 refrigerantes**
2. Funcionário acessa **Registrar Saída**
3. Busca produto **Refrigerante Cola 2L**
4. Digita quantidade **10**
5. Sistema verifica estoque **5 unidades**
6. Sistema exibe mensagem:


Quantidade indisponível em estoque.
Saldo atual: 5 unidades.


7. Funcionário ajusta venda ou informa o cliente.

---

# 13. Obstáculos e Riscos

- **Resistência da dona**  
  Pode preferir continuar usando planilhas

- **Dificuldade com tecnologia**  
  Funcionários podem ter dificuldade inicial

- **Dados inconsistentes na migração**  
  Planilhas atuais podem conter erros

- **Esquecer de registrar saídas**  
  Estoque pode ficar incorreto

- **Prazo curto de desenvolvimento**  
  Implementar todos os casos de uso em poucas semanas
