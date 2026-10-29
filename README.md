Atividade G1 - Trabalho de Banco de Dados — UPA Monitor

Alunos: Danielly Magno Barbosa; Gabriel Lima Rosa; Wellington Pereira do Nascimento

# QUESTÃO 1 — Modelagem de Dados com MERMAID

<img src="Captura de tela 2026-10-28 221546.png">

## QUESTÃO 2 — O Desafio do "Prompt Inverso"

### Criação das tabelas

```sql
CREATE TABLE upa (
    id_upa INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nome   VARCHAR(80) NOT NULL UNIQUE,
    ativa  BOOLEAN NOT NULL DEFAULT TRUE
);

CREATE TABLE paciente (
    id_paciente   INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    cns           VARCHAR(15) NOT NULL UNIQUE,
    nome          VARCHAR(120) NOT NULL,
    dt_nascimento DATE
);

CREATE TABLE classificacao (
    id_classificacao INT PRIMARY KEY,
    nome  VARCHAR(30) NOT NULL UNIQUE,
    ordem INT NOT NULL
);

CREATE TABLE setor (
    id_setor INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nome     VARCHAR(60) NOT NULL UNIQUE
);

CREATE TABLE atendimento (
    id_atendimento   INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    id_upa           INT NOT NULL REFERENCES upa(id_upa),
    id_paciente      INT NOT NULL REFERENCES paciente(id_paciente),
    id_classificacao INT REFERENCES classificacao(id_classificacao)
);

CREATE TABLE movimentacao (
    id_atendimento INT NOT NULL REFERENCES atendimento(id_atendimento),
    nr_sequencia   INT NOT NULL,
    id_setor       INT NOT NULL REFERENCES setor(id_setor),
    dt_inicio      TIMESTAMP NOT NULL,
    dt_fim         TIMESTAMP,
    PRIMARY KEY (id_atendimento, nr_sequencia)
);
```

### Dados de apoio

```sql
INSERT INTO classificacao VALUES
 (1,'Emergência',1),(2,'Muito urgente',2),(3,'Urgente',3),
 (4,'Pouco urgente',4),(5,'Não urgente',5);

INSERT INTO setor (nome) VALUES
 ('Aguardando Triagem'),('Pacientes Triados'),('Atendidos Consultório'),
 ('Sutura'),('Sala Vermelha'),('Observação Masculina'),
 ('Observação Feminina'),('Observação Infantil'),('Medicação Administrada'),
 ('Exames Laboratório'),('Exames Radiologia'),('Odontologia'),
 ('Atendimento Pediátrico'),('Assistência Social'),('Transferências');
```

## Link da conversa com a Inteligência Artificial: 

https://claude.ai/share/7cebf66f-627b-4140-97f6-5d7c2563061e
