CREATE TABLE cliente (
    Data_de_Nascimento DATE,
    Endereco VARCHAR,
    Estado_Civil VARCHAR,
    Ocupacao_Atual VARCHAR,
    Renda_Mensal FLOAT,
    Sexo VARCHAR,
    RG CHAR,
    Nome VARCHAR,
    CPF CHAR,
    id_cliente CHAR PRIMARY KEY
);
 
SELECT * FROM cliente;
 
CREATE TABLE Apolice (
    Tipo_de_Plano VARCHAR,
    Porcentagem DECIMAL,
    Mensalidade FLOAT,
    Valor_da_Indenizacao FLOAT,
    Peso FLOAT,
    Forma_de_Pagamento VARCHAR,
    id_apolice CHAR,
    id_funcionario CHAR,
    Altura DECIMAL,
    fk_cliente_id_cliente CHAR,
    fk_Corretor_id_funcionario CHAR,
    PRIMARY KEY (id_apolice, id_funcionario)
);
 
SELECT * FROM Apolice;
 
 
CREATE TABLE Beneficiario (
    Data_de_Nascimento DATE,
    Endereco VARCHAR,
    Sexo VARCHAR,
    RG CHAR,
    Nome VARCHAR,
    Grau_de_Parentesco VARCHAR,
    CPF CHAR,
    fk_Apolice_id_apolice CHAR,
    fk_Apolice_id_funcionario CHAR
);
 
SELECT * FROM Beneficiario;
 
CREATE TABLE Corretor (
    Nome VARCHAR,
    Sexo VARCHAR,
    RG CHAR,
    CPF CHAR,
    Data_de_Nascimento DATE,
    Telefone FLOAT,
    Cargo VARCHAR,
    Dados_Bancarios FLOAT,
    id_funcionario CHAR PRIMARY KEY
);
 
SELECT * FROM Corretor;
 
CREATE TABLE Boleto_Nota_Fiscal (
    Data_de_Emissao DATE,
    Razao_Social VARCHAR,
    Endereco VARCHAR,
    CNPJ CHAR,
    id_identificador CHAR PRIMARY KEY,
    Valor DECIMAL,
);
 
SELECT * FROM Boleto_Nota_Fiscal;
 
CREATE TABLE Emite (
    fk_Apolice_id_apolice CHAR,
    fk_Apolice_id_funcionario CHAR,
    fk_Boleto_Nota_Fiscal_id_identificador CHAR
);
 
SELECT * FROM Emite;
 
ALTER TABLE Apolice ADD CONSTRAINT FK_Apolice_2
    FOREIGN KEY (fk_cliente_id_cliente)
    REFERENCES cliente (id_cliente);
 
ALTER TABLE Apolice ADD CONSTRAINT FK_Apolice_3
    FOREIGN KEY (fk_Corretor_id_funcionario)
    REFERENCES Corretor (id_funcionario);
 
ALTER TABLE Beneficiario ADD CONSTRAINT FK_Beneficiario_1
    FOREIGN KEY (fk_Apolice_id_apolice, fk_Apolice_id_funcionario)
    REFERENCES Apolice (id_apolice, id_funcionario);
 
ALTER TABLE Emite ADD CONSTRAINT FK_Emite_1
