Projeto de Banco de Dados: E-commerce 🛒

Este repositório contém o modelo conceitual e lógico de um banco de dados para um sistema de e-commerce. O projeto foi desenvolvido com foco na estruturação robusta das entidades e em garantir que o fluxo de ponta a ponta — desde o fornecimento até a entrega do pedido ao cliente final — siga as melhores práticas de normalização.

📖 Contexto do Projeto

Este esquema de banco de dados modela a arquitetura de um e-commerce completo. O fluxo mapeia a jornada desde o armazenamento de produtos de fornecedores e vendedores terceirizados (modelo marketplace) até a gestão de estoque e o processamento de compras.

O modelo inicial foi refinado para atender a requisitos essenciais de regras de negócios, suportando uma categorização rigorosa de clientes, flexibilidade de faturamento e rastreamento logístico detalhado.

🚀 Soluções Arquiteturais e Refinamentos

Para atender às regras de negócio exigidas pelo desafio do projeto, as seguintes implementações foram feitas:

1. Separação de Cliente PJ e PF (Especialização)

Para garantir que uma conta seja Pessoa Física (PF) ou Pessoa Jurídica (PJ) de forma mutuamente exclusiva, aplicou-se o conceito de especialização.
A tabela original Cliente atua como uma superclasse contendo atributos genéricos (como endereço). A partir dela, derivam-se duas subclasses em relações 1:1:

Cliente_pf: Contém CPF e Nome.

Cliente_pj: Contém CNPJ e Razão Social.
Isso elimina a inserção de dados nulos que ocorreriam ao manter atributos de ambos os tipos em uma única tabela.

2. Gerenciamento de Formas de Pagamento

Para atender ao requisito de múltiplos métodos de pagamento cadastrados, foi criada a entidade Forma_de_pagamento.
A relação modelada é de 1:N com a entidade Cliente, ou seja, a conta do usuário atua como uma "carteira digital" onde ele pode cadastrar vários cartões ou chaves PIX. A entidade Pedido recebe uma chave estrangeira dessa tabela para registrar exatamente qual foi o método selecionado no momento daquela transação específica.

3. Módulo de Entrega e Rastreio

Para isolar a logística do fechamento da compra, criou-se a entidade Entrega com os atributos status_entrega e codigo_rastreio.
A relação com a tabela Pedido é de 1:N, o que garante flexibilidade para envios fracionados (split shipment), permitindo que itens de um mesmo pedido, oriundos de vendedores terceirizados diferentes, gerem códigos de rastreio e status independentes.

🗂️ Estrutura de Entidades Principais

Cliente: Gerencia os dados do usuário, especializando-se em PF ou PJ.

Produto: Entidade central do catálogo do e-commerce.

Pedido: Consolida a transação, unindo Cliente, Forma de Pagamento e os Produtos escolhidos.

Fornecedor / Terceiro-Vendedor: Abastecem o catálogo de produtos (relação N:M com Produto).

Estoque: Gerencia o armazenamento físico e as quantidades dos produtos.

Entrega: Monitora o fluxo logístico pós-compra.

🛠️ Ferramentas Utilizadas

MySQL Workbench: Utilizado para a criação do Diagrama Entidade-Relacionamento (DER) e modelagem relacional.
