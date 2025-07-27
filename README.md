# 📦 Sistema de Gerenciamento de Pedidos - Criação do Banco de Dados

Este projeto consiste na criação de um banco de dados relacional para um sistema de gerenciamento de pedidos de uma pequena loja. A estrutura foi definida com base em boas práticas de modelagem, uso adequado de tipos de dados, definição de chaves primárias e estrangeiras, além de relacionamentos entre as tabelas.

---

## 🧱 Estrutura e Scripts SQL

### 🗂️ Tabela: Categoria

CREATE TABLE categoria (
  id_categoria INT PRIMARY KEY AUTO_INCREMENT,
  descricao VARCHAR(100) NOT NULL
);

**Tabela: UF**

CREATE TABLE uf (

  id_uf INT PRIMARY KEY AUTO_INCREMENT,
  
  sigla VARCHAR(2) NOT NULL,
  
  descricao VARCHAR(50) NOT NULL
  
);

**Tabela: Cidade**

CREATE TABLE cidade (

  id_cidade INT PRIMARY KEY AUTO_INCREMENT,
  
  id_uf INT NOT NULL,
  
  descricao VARCHAR(100) NOT NULL,
  
  FOREIGN KEY (id_uf) REFERENCES uf(id_uf)
  
);

**Tabela: Produtos**

CREATE TABLE produtos (

  id_produto INT PRIMARY KEY AUTO_INCREMENT,
  
  descricao VARCHAR(150) NOT NULL,
  
  id_categoria INT NOT NULL,
  
  preco_unitario DECIMAL(10, 2) NOT NULL,
  
  quantidade_estoque INT NOT NULL,
  
  observacoes TEXT,
  
  FOREIGN KEY (id_categoria) REFERENCES categoria(id_categoria)
  
);

**Tabela: Clientes**

CREATE TABLE clientes (

  id_cliente INT PRIMARY KEY AUTO_INCREMENT,
  
  nome_completo VARCHAR(150) NOT NULL,
  
  cpf_cnpj VARCHAR(18) NOT NULL,
  
  telefone VARCHAR(20),
  
  email VARCHAR(100),
  
  endereco VARCHAR(200),
  
  id_uf INT NOT NULL,
  
  id_cidade INT NOT NULL,
  
  cep VARCHAR(10),
  
  FOREIGN KEY (id_uf) REFERENCES uf(id_uf),
  
  FOREIGN KEY (id_cidade) REFERENCES cidade(id_cidade)
  
);

**Tabela: Pedidos**

CREATE TABLE pedidos (

  id_pedido INT PRIMARY KEY AUTO_INCREMENT,
  
  id_cliente INT NOT NULL,
  
  data_pedido DATE NOT NULL,
  
  total_pedido DECIMAL(10, 2) NOT NULL,
  
  FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
  
);

**Tabela: Pedidos_Produtos**

CREATE TABLE pedidos_produtos (

  id INT PRIMARY KEY AUTO_INCREMENT,
  
  id_pedido INT NOT NULL,
  
  id_produto INT NOT NULL,
  
  referencia VARCHAR(50),
  
  descricao VARCHAR(150),
  
  quantidade INT NOT NULL,
  
  valor_unitario DECIMAL(10, 2) NOT NULL,
  
  valor_total DECIMAL(10, 2) NOT NULL,
  
  FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
  
  FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
  
);

### 💼 Caso de Uso

Ideal para sistemas comerciais, ERP básico ou lojas locais que desejam iniciar a digitalização da operação com controle eficiente de pedidos, estoque e cadastro de clientes.

### 🚀 Tecnologias e Conceitos Utilizados

✅ SQL Puro (MySQL, PostgreSQL ou SQL Server)

✅ Modelagem relacional

✅ Normalização de dados

✅ Relacionamentos 1:N e N:N

✅ Chaves primárias e estrangeiras

✅ Tipagem forte e integridade referencial

### 👨‍💻 Autor
Desenvolvido por Guilherme dos Santos
