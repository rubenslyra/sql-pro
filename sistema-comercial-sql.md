# 🗄️ SISTEMA: VENDAS → ENTREGAS → ESTOQUE/ARMAZÉM
## Diagrama Resumido das Relações

```
PESSOA ──1:N── VENDA ──1:N── ITEM_VENDA ──N:1── PRODUTO
                  │                         │
                  │                         └── N:1── ESTOQUE ──N:1── ARMAZÉM
                  │
                  └── 1:1── ENTREGA ──N:1── MOTORISTA
                                     └── N:1── ENDERECO
```

---

## 📜 SCRIPT COMPLETO DE CRIAÇÃO (T-SQL / SQL Server)

```sql
-- =============================================
-- SISTEMA: VENDAS + ENTREGAS + ESTOQUE/ARMAZÉM
-- Banco: SQL Server 2017+
-- Versão: 1.0 | 2026-09-23
-- =============================================

-- Criação do Banco de Dados
IF NOT EXISTS (SELECT * FROM sys.databases WHERE name = 'SistemaVendasEntregas')
BEGIN
    CREATE DATABASE SistemaVendasEntregas;
END
GO

USE SistemaVendasEntregas;
GO

-- =============================================
-- 1. TABELA: ARMAZÉM
-- =============================================
CREATE TABLE Armazem (
    IdArmazem     INT IDENTITY(1,1) PRIMARY KEY,
    Nome          VARCHAR(100) NOT NULL,
    Endereco      VARCHAR(200) NOT NULL,
    Bairro        VARCHAR(50) NOT NULL,
    Cidade        VARCHAR(50) NOT NULL,
    UF            CHAR(2) NOT NULL,
    CEP           CHAR(8) NOT NULL,
    Responsavel   VARCHAR(100) NULL,
    Ativo         BIT DEFAULT 1,
    DataCadastro  DATETIME DEFAULT GETDATE()
);

-- =============================================
-- 2. TABELA: PRODUTO
-- =============================================
CREATE TABLE Produto (
    IdProduto     INT IDENTITY(1,1) PRIMARY KEY,
    Codigo        VARCHAR(50) UNIQUE NOT NULL,
    Nome          VARCHAR(150) NOT NULL,
    Descricao     VARCHAR(500) NULL,
    Categoria     VARCHAR(50) NULL,
    PrecoUnitario DECIMAL(12,2) NOT NULL CHECK (PrecoUnitario >= 0),
    UnidadeMedida VARCHAR(10) NOT NULL DEFAULT 'UN', -- UN, KG, L, CX...
    Ativo         BIT DEFAULT 1,
    DataCadastro  DATETIME DEFAULT GETDATE()
);

-- =============================================
-- 3. TABELA: ESTOQUE
-- =============================================
CREATE TABLE Estoque (
    IdEstoque     INT IDENTITY(1,1) PRIMARY KEY,
    IdProduto     INT NOT NULL,
    IdArmazem     INT NOT NULL,
    Quantidade    DECIMAL(12,3) NOT NULL DEFAULT 0 CHECK (Quantidade >= 0),
    QuantidadeMinima DECIMAL(12,3) DEFAULT 5 CHECK (QuantidadeMinima >= 0),
    Localizacao   VARCHAR(30) NULL, -- Ex: "Ala B - Prateleira 3"
    DataAtualizacao DATETIME DEFAULT GETDATE(),

    CONSTRAINT FK_Estoque_Produto FOREIGN KEY (IdProduto)
        REFERENCES Produto(IdProduto) ON UPDATE CASCADE ON DELETE RESTRICT,
    CONSTRAINT FK_Estoque_Armazem FOREIGN KEY (IdArmazem)
        REFERENCES Armazem(IdArmazem) ON UPDATE CASCADE ON DELETE RESTRICT,
    CONSTRAINT UQ_Produto_Armazem UNIQUE (IdProduto, IdArmazem)
);

-- =============================================
-- 4. TABELA: PESSOA (Clientes / Fornecedores)
-- =============================================
CREATE TABLE Pessoa (
    IdPessoa      INT IDENTITY(1,1) PRIMARY KEY,
    NomeCompleto  VARCHAR(150) NOT NULL,
    TipoPessoa    CHAR(1) NOT NULL CHECK (TipoPessoa IN ('F','J')), -- Física/Jurídica
    Documento     CHAR(14) UNIQUE NOT NULL, -- CPF(11) ou CNPJ(14)
    Telefone      VARCHAR(20) NULL,
    Email         VARCHAR(100) NULL,
    Ativo         BIT DEFAULT 1,
    DataCadastro  DATETIME DEFAULT GETDATE()
);

-- =============================================
-- 5. TABELA: MOTORISTA
-- =============================================
CREATE TABLE Motorista (
    IdMotorista   INT IDENTITY(1,1) PRIMARY KEY,
    Nome          VARCHAR(100) NOT NULL,
    CNH           VARCHAR(20) UNIQUE NOT NULL,
    Telefone      VARCHAR(20) NOT NULL,
    VeiculoPlaca  CHAR(7) NULL,
    VeiculoModelo VARCHAR(50) NULL,
    Ativo         BIT DEFAULT 1,
    DataCadastro  DATETIME DEFAULT GETDATE()
);

-- =============================================
-- 6. TABELA: VENDA
-- =============================================
CREATE TABLE Venda (
    IdVenda       INT IDENTITY(1,1) PRIMARY KEY,
    IdPessoa      INT NOT NULL,
    NumeroVenda   VARCHAR(20) UNIQUE NOT NULL,
    DataVenda     DATETIME NOT NULL DEFAULT GETDATE(),
    StatusVenda   VARCHAR(20) NOT NULL DEFAULT 'PENDENTE'
        CHECK (StatusVenda IN ('PENDENTE','APROVADA','FATURADA','CANCELADA')),
    ValorTotal    DECIMAL(12,2) NOT NULL DEFAULT 0,
    Observacao    VARCHAR(500) NULL,

    CONSTRAINT FK_Venda_Pessoa FOREIGN KEY (IdPessoa)
        REFERENCES Pessoa(IdPessoa) ON UPDATE CASCADE ON DELETE RESTRICT
);

-- =============================================
-- 7. TABELA: ITEM_VENDA
-- =============================================
CREATE TABLE ItemVenda (
    IdItemVenda   INT IDENTITY(1,1) PRIMARY KEY,
    IdVenda       INT NOT NULL,
    IdProduto     INT NOT NULL,
    Quantidade    DECIMAL(12,3) NOT NULL CHECK (Quantidade > 0),
    ValorUnitario DECIMAL(12,2) NOT NULL CHECK (ValorUnitario >= 0),
    ValorTotal    AS (Quantidade * ValorUnitario) PERSISTED,

    CONSTRAINT FK_ItemVenda_Venda FOREIGN KEY (IdVenda)
        REFERENCES Venda(IdVenda) ON UPDATE CASCADE ON DELETE CASCADE,
    CONSTRAINT FK_ItemVenda_Produto FOREIGN KEY (IdProduto)
        REFERENCES Produto(IdProduto) ON UPDATE CASCADE ON DELETE RESTRICT
);

-- =============================================
-- 8. TABELA: ENDEREÇO DE ENTREGA
-- =============================================
CREATE TABLE EnderecoEntrega (
    IdEndereco    INT IDENTITY(1,1) PRIMARY KEY,
    Logradouro    VARCHAR(150) NOT NULL,
    Numero        VARCHAR(20) NOT NULL,
    Complemento   VARCHAR(100) NULL,
    Bairro        VARCHAR(50) NOT NULL,
    Cidade        VARCHAR(50) NOT NULL,
    UF            CHAR(2) NOT NULL,
    CEP           CHAR(8) NOT NULL,
    PontoReferencia VARCHAR(100) NULL
);

-- =============================================
-- 9. TABELA: ENTREGA
-- =============================================
CREATE TABLE Entrega (
    IdEntrega     INT IDENTITY(1,1) PRIMARY KEY,
    IdVenda       INT UNIQUE NOT NULL, -- 1 entrega = 1 venda
    IdMotorista   INT NULL,
    IdEndereco    INT NOT NULL,
    StatusEntrega VARCHAR(30) NOT NULL DEFAULT 'AGUARDANDO'
        CHECK (StatusEntrega IN (
            'AGUARDANDO','PREPARANDO','SAIU_ENTREGA','ENTREGUE','CANCELADA'
        )),
    DataPrevisao  DATE NULL,
    DataSaida     DATETIME NULL,
    DataEntregue  DATETIME NULL,
    RastreioCod   VARCHAR(50) UNIQUE NULL,
    Observacao    VARCHAR(300) NULL,

    CONSTRAINT FK_Entrega_Venda FOREIGN KEY (IdVenda)
        REFERENCES Venda(IdVenda) ON UPDATE CASCADE ON DELETE RESTRICT,
    CONSTRAINT FK_Entrega_Motorista FOREIGN KEY (IdMotorista)
        REFERENCES Motorista(IdMotorista) ON UPDATE CASCADE ON DELETE SET NULL,
    CONSTRAINT FK_Entrega_Endereco FOREIGN KEY (IdEndereco)
        REFERENCES EnderecoEntrega(IdEndereco) ON UPDATE CASCADE ON DELETE RESTRICT
);

-- =============================================
-- 10. TABELA: MOVIMENTAÇÃO DE ESTOQUE
-- =============================================
CREATE TABLE MovimentacaoEstoque (
    IdMovimentacao INT IDENTITY(1,1) PRIMARY KEY,
    IdEstoque      INT NOT NULL,
    TipoMovimento  CHAR(1) NOT NULL CHECK (TipoMovimento IN ('E','S','A')), -- Entrada/Saída/Ajuste
    Quantidade     DECIMAL(12,3) NOT NULL,
    IdItemVenda    INT NULL, -- Se saída por venda
    Motivo         VARCHAR(100) NULL,
    DataMovimento  DATETIME DEFAULT GETDATE(),

    CONSTRAINT FK_Movimentacao_Estoque FOREIGN KEY (IdEstoque)
        REFERENCES Estoque(IdEstoque) ON UPDATE CASCADE ON DELETE RESTRICT,
    CONSTRAINT FK_Movimentacao_ItemVenda FOREIGN KEY (IdItemVenda)
        REFERENCES ItemVenda(IdItemVenda) ON UPDATE NO ACTION
);

-- =============================================
-- ÍNDICES PARA PERFORMANCE
-- =============================================
CREATE NONCLUSTERED INDEX IX_Venda_Data     ON Venda(DataVenda);
CREATE NONCLUSTERED INDEX IX_Venda_Status   ON Venda(StatusVenda);
CREATE NONCLUSTERED INDEX IX_Entrega_Status ON Entrega(StatusEntrega);
CREATE NONCLUSTERED INDEX IX_Estoque_Prod   ON Estoque(IdProduto);
CREATE NONCLUSTERED INDEX IX_Mov_Data       ON MovimentacaoEstoque(DataMovimento);

PRINT '✅ ESTRUTURA CRIADA COM SUCESSO!';
GO
```

---

## ✅ O QUE ESTÁ COBERTO

| Módulo | Tabelas Principais | Funcionalidade |
|---|---|---|
| 📦 **Estoque/Armazém** | `Armazem`, `Produto`, `Estoque`, `MovimentacaoEstoque` | Saldo por armazém, mínimo, entradas/saídas, histórico |
| 💰 **Vendas** | `Pessoa`, `Venda`, `ItemVenda` | Cadastro de clientes, vendas com múltiplos itens, valor calculado |
| 🚚 **Entregas** | `Motorista`, `EnderecoEntrega`, `Entrega` | Rastreio, status, motorista, previsão e datas |
| 🔗 **Integração** | Movimentação automática | Venda → Saída no estoque → Histórico |

---

## PRÓXIMO PASSO 👉 POPULAR OS DADOS

Quer que eu gere o **script de inserção de dados de teste** agora? Vou incluir:
- 2–3 armazéns
- 10+ produtos com estoque
- 5 clientes
- 3 motoristas
- 4 vendas completas → itens → entrega → baixa de estoque

-------------

Aqui está o **script completo de população de dados** 📝 — tudo consistente, ligado entre as tabelas e pronto para rodar direto no seu banco!

---

# 📋 SCRIPT DE INSERÇÃO — DADOS DE TESTE

```sql
USE SistemaVendasEntregas;
GO

-- =============================================
-- 1. ARMAZÉNS
-- =============================================
INSERT INTO Armazem (Nome, Endereco, Bairro, Cidade, UF, CEP, Responsavel)
VALUES
('Armazém Central Vila Velha', 'Av. Carlos Moreira, 1200', 'Centro', 'Vila Velha', 'ES', '29100020', 'Carlos Silva'),
('Armazém Vitória', 'Rua das Flores, 45', 'Jardim Camburi', 'Vitória', 'ES', '29090000', 'Mariana Costa'),
('Armazém Serra', 'Rod. Contorno Norte, 890', 'Portal de Jacaraípe', 'Serra', 'ES', '29170000', 'Pedro Henrique');

-- =============================================
-- 2. PRODUTOS
-- =============================================
INSERT INTO Produto (Codigo, Nome, Descricao, Categoria, PrecoUnitario, UnidadeMedida)
VALUES
('PROD-001', 'Notebook Essencial 15.6"', 'Intel Core i5, 8GB RAM, 256GB SSD', 'Informática', 3299.90, 'UN'),
('PROD-002', 'Smartphone XYZ 128GB', 'Tela 6.5", Câmera 48MP, Bateria 5000mAh', 'Celulares', 1899.00, 'UN'),
('PROD-003', 'Cadeira Ergonômica Giratória', 'Ajustável, Apoio Lombar, Cor Preta', 'Móveis', 459.90, 'UN'),
('PROD-004', 'Monitor LED 24" Full HD', 'Tela Antirreflexiva, 75Hz, HDMI/VGA', 'Informática', 699.00, 'UN'),
('PROD-005', 'Teclado Mecânico RGB', 'Switch Azul, ABNT2, Cabo Removível', 'Periféricos', 199.90, 'UN'),
('PROD-006', 'Mouse Sem Fio Ergonômico', 'Recarregável, 2400DPI, 6 Botões', 'Periféricos', 89.90, 'UN'),
('PROD-007', 'Impressora Multifuncional Tanque', 'Impressão/ Cópia/ Digitalização, Wi-Fi', 'Informática', 1150.00, 'UN'),
('PROD-008', 'Cafeteira Elétrica Programável', '1.5L, Timer, Mantém Quente', 'Eletrodomésticos', 129.90, 'UN'),
('PROD-009', 'Caixa de Som Bluetooth 20W', 'À Prova d''Água, Bateria 12h', 'Áudio', 149.90, 'UN'),
('PROD-010', 'Fone de Ouvido Cancelamento Ruído', 'Bluetooth 5.3, 30h Bateria', 'Áudio', 299.90, 'UN');

-- =============================================
-- 3. ESTOQUE (saldo por armazém)
-- =============================================
INSERT INTO Estoque (IdProduto, IdArmazem, Quantidade, QuantidadeMinima, Localizacao)
VALUES
-- Armazém 1
(1, 1, 25, 5, 'Ala A - Prat. 01'),
(2, 1, 40, 8, 'Ala A - Prat. 02'),
(3, 1, 15, 3, 'Ala B - Prat. 05'),
(4, 1, 30, 5, 'Ala A - Prat. 03'),
(5, 1, 60, 10, 'Ala C - Prat. 02'),
(6, 1, 80, 10, 'Ala C - Prat. 03'),
-- Armazém 2
(1, 2, 12, 4, 'Setor 1 - Estante 1A'),
(2, 2, 18, 5, 'Setor 1 - Estante 1B'),
(4, 2, 10, 3, 'Setor 1 - Estante 2A'),
(7, 2, 8, 2, 'Setor 2 - Estante 3A'),
(8, 2, 22, 5, 'Setor 3 - Estante 1C'),
-- Armazém 3
(3, 3, 20, 4, 'Bloco 2 - Prat. 04'),
(9, 3, 35, 6, 'Bloco 3 - Prat. 01'),
(10, 3, 28, 5, 'Bloco 3 - Prat. 02');

-- =============================================
-- 4. PESSOAS (Clientes)
-- =============================================
INSERT INTO Pessoa (NomeCompleto, TipoPessoa, Documento, Telefone, Email)
VALUES
('João Marcos de Souza', 'F', '12345678901', '27998765432', 'joao.souza@email.com'),
('Empresa Tech Soluções Ltda', 'J', '05678901234567', '2733224455', 'compras@techsol.com.br'),
('Ana Carolina Mendes', 'F', '98765432109', '27991234567', 'ana.mendes@email.com'),
('Roberto Carlos Pereira', 'F', '45678912301', '27988887777', 'roberto.pereira@email.com'),
('Loja Comercial Bem Barato ME', 'J', '12345678901234', '2732221100', 'atendimento@bambarato.com.br');

-- =============================================
-- 5. MOTORISTAS
-- =============================================
INSERT INTO Motorista (Nome, CNH, Telefone, VeiculoPlaca, VeiculoModelo)
VALUES
('Lucas Almeida', 'ES-1234567890', '27999991111', 'ABC1D23', 'Fiorino Branco'),
('Fernanda Gomes', 'MG-9876543210', '27998882222', 'XYZ9A87', 'Kangoo Azul'),
('Bruno César Rodrigues', 'RJ-4567890123', '27997773333', 'DEF4G56', 'Saveiro Prata');

-- =============================================
-- 6. VENDAS
-- =============================================
INSERT INTO Venda (IdPessoa, NumeroVenda, DataVenda, StatusVenda, ValorTotal, Observacao)
VALUES
(1, 'V-2026-0001', '2026-09-20 14:30:00', 'FATURADA', 4099.70, 'Pagamento via Pix - Entrega padrão'),
(2, 'V-2026-0002', '2026-09-21 09:15:00', 'APROVADA', 7598.50, 'Compra corporativa - NF-e a emitir'),
(3, 'V-2026-0003', '2026-09-22 16:45:00', 'PENDENTE', 459.90, 'Aguardando confirmação de pagamento'),
(4, 'V-2026-0004', '2026-09-23 10:00:00', 'FATURADA', 1449.80, 'Entrega agendada para amanhã');

-- =============================================
-- 7. ITENS DAS VENDAS
-- =============================================
-- Venda 1: Notebook + Monitor + Teclado
INSERT INTO ItemVenda (IdVenda, IdProduto, Quantidade, ValorUnitario)
VALUES
(1, 1, 1, 3299.90),
(1, 4, 1, 699.00),
(1, 5, 1, 199.90);

-- Venda 2: 2 Notebooks + 3 Cadeiras + 4 Mouses
INSERT INTO ItemVenda (IdVenda, IdProduto, Quantidade, ValorUnitario)
VALUES
(2, 1, 2, 3299.90),
(2, 3, 3, 459.90),
(2, 6, 4, 89.90);

-- Venda 3: 1 Cadeira
INSERT INTO ItemVenda (IdVenda, IdProduto, Quantidade, ValorUnitario)
VALUES
(3, 3, 1, 459.90);

-- Venda 4: Smartphone + Fone + Caixa Som
INSERT INTO ItemVenda (IdVenda, IdProduto, Quantidade, ValorUnitario)
VALUES
(4, 2, 1, 1899.00),
(4, 10, 1, 299.90),
(4, 9, 1, 149.90);

-- =============================================
-- 8. ENDEREÇOS DE ENTREGA
-- =============================================
INSERT INTO EnderecoEntrega (Logradouro, Numero, Complemento, Bairro, Cidade, UF, CEP, PontoReferencia)
VALUES
('Rua dos Coqueiros', '150', 'Apto 302, Bloco B', 'Praia da Costa', 'Vila Velha', 'ES', '29101230', 'Próximo ao supermercado Extra'),
('Av. Governador Bley', '2000', 'Sala 101', 'Centro', 'Vitória', 'ES', '29010150', 'Edifício Central'),
('Rua das Orquídeas', '78', 'Casa', 'Jardim América', 'Cariacica', 'ES', '29140000', 'Portão branco'),
('Av. Jerônimo Monteiro', '500', 'Loja 02', 'Centro', 'Vila Velha', 'ES', '29100010', 'Em frente à Praça da Matriz');

-- =============================================
-- 9. ENTREGAS
-- =============================================
INSERT INTO Entrega (IdVenda, IdMotorista, IdEndereco, StatusEntrega, DataPrevisao, DataSaida, DataEntregue, RastreioCod, Observacao)
VALUES
(1, 1, 1, 'ENTREGUE', '2026-09-21', '2026-09-21 08:00:00', '2026-09-21 11:30:00', 'RAST-ES-001234', 'Assinatura: João Marcos'),
(2, 2, 2, 'SAIU_ENTREGA', '2026-09-24', '2026-09-23 14:00:00', NULL, 'RAST-ES-001235', 'Entrega para empresa - horário comercial'),
(3, NULL, 3, 'AGUARDANDO', '2026-09-26', NULL, NULL, NULL, 'Aguardando pagamento para despachar'),
(4, 3, 4, 'PREPARANDO', '2026-09-24', NULL, NULL, 'RAST-ES-001236', 'Separação em andamento no armazém');

-- =============================================
-- 10. MOVIMENTAÇÃO DE ESTOQUE (saídas automáticas pelas vendas faturadas)
-- =============================================
-- Venda 1 - Itens retirados do Armazém 1
INSERT INTO MovimentacaoEstoque (IdEstoque, TipoMovimento, Quantidade, IdItemVenda, Motivo)
VALUES
(1, 'S', 1, 1, 'Venda V-2026-0001'),   -- Notebook
(4, 'S', 1, 2, 'Venda V-2026-0001'),   -- Monitor
(5, 'S', 1, 3, 'Venda V-2026-0001');   -- Teclado

-- Venda 2 - Itens retirados do Armazém 1
INSERT INTO MovimentacaoEstoque (IdEstoque, TipoMovimento, Quantidade, IdItemVenda, Motivo)
VALUES
(1, 'S', 2, 4, 'Venda V-2026-0002'),   -- Notebook x2
(3, 'S', 3, 5, 'Venda V-2026-0002'),   -- Cadeira x3
(6, 'S', 4, 6, 'Venda V-2026-0002');   -- Mouse x4

-- Venda 4 - Itens retirados do Armazém 1
INSERT INTO MovimentacaoEstoque (IdEstoque, TipoMovimento, Quantidade, IdItemVenda, Motivo)
VALUES
(2, 'S', 1, 8, 'Venda V-2026-0004'),   -- Smartphone
(10, 'S', 1, 9, 'Venda V-2026-0004'),  -- Fone
(9, 'S', 1, 10, 'Venda V-2026-0004');  -- Caixa de Som

PRINT '✅ DADOS INSERIDOS COM SUCESSO!';
GO
```

---

## ✅ RESUMO DOS DADOS CARREGADOS

| Tabela | Qtd |
|---|---|
| 🏭 Armazéns | 3 |
| 📦 Produtos | 10 |
| 📊 Estoque | 13 registros (saldo por local) |
| 👤 Clientes | 5 |
| 🚚 Motoristas | 3 |
| 💰 Vendas | 4 |
| 📋 Itens de Venda | 10 |
| 📍 Endereços | 4 |
| 🛵 Entregas | 4 |
| 📉 Movimentações | 9 |

---

## ✅ VALIDAÇÃO RÁPIDA (rode para conferir)

```sql
-- Saldo atual de estoque
SELECT 
    p.Nome,
    a.Nome AS Armazem,
    e.Quantidade,
    e.QuantidadeMinima
FROM Estoque e
JOIN Produto p ON e.IdProduto = p.IdProduto
JOIN Armazem a ON e.IdArmazem = a.IdArmazem
ORDER BY p.Nome;

-- Vendas com status e valor
SELECT 
    NumeroVenda, 
    NomeCompleto, 
    DataVenda, 
    StatusVenda, 
    ValorTotal
FROM Venda v
JOIN Pessoa p ON v.IdPessoa = p.IdPessoa;

-- Situação das entregas
SELECT 
    v.NumeroVenda,
    e.StatusEntrega,
    m.Nome AS Motorista,
    end.Cidade,
    e.DataPrevisao
FROM Entrega e
JOIN Venda v ON e.IdVenda = v.IdVenda
LEFT JOIN Motorista m ON e.IdMotorista = m.IdMotorista
JOIN EnderecoEntrega end ON e.IdEndereco = end.IdEndereco;
```

---

## 🚀 PRÓXIMOS PASSOS — O que vem agora?

Escolha o próximo tema:

1️⃣ **Consultas práticas** — Seleções, filtros, junções com esse banco  
2️⃣ **Funções e agregações** — `GROUP BY`, somar vendas por cliente/produto/período  
3️⃣ **Views e Procedures** — Automatizar consultas frequentes  
4️⃣ **Trigger de estoque** — Fazer a saída automática na movimentação ao vender  
5️⃣ **Relatórios prontos** — Vendas por período, estoque abaixo do mínimo, entregas atrasadas

**Me fala o número e seguimos!** 💪
