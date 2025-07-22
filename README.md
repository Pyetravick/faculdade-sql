# faculdade-sql
CREATE DATABASE IF NOT EXISTS faculdadedb;
USE faculdadedb;

DROP TABLE IF EXISTS matricula;
DROP TABLE IF EXISTS turma;
DROP TABLE IF EXISTS curso_disciplina;
DROP TABLE IF EXISTS disciplina;
DROP TABLE IF EXISTS curso;
DROP TABLE IF EXISTS professor;
DROP TABLE IF EXISTS aluno;

CREATE TABLE aluno (
    id_aluno INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    data_nascimento DATE NOT NULL
);

CREATE TABLE professor (
    id_professor INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    especialidade VARCHAR(100) NOT NULL
);

CREATE TABLE curso (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nome_curso VARCHAR(100) NOT NULL,
    duracao INT NOT NULL
);

CREATE TABLE disciplina (
    id_disciplina INT AUTO_INCREMENT PRIMARY KEY,
    nome_disciplina VARCHAR(100) NOT NULL,
    carga_horaria INT NOT NULL
);

CREATE TABLE curso_disciplina (
    id_curso INT,
    id_disciplina INT,
    PRIMARY KEY (id_curso, id_disciplina),
    FOREIGN KEY (id_curso) REFERENCES curso(id_curso),
    FOREIGN KEY (id_disciplina) REFERENCES disciplina(id_disciplina)
);

CREATE TABLE turma (
    id_turma INT AUTO_INCREMENT PRIMARY KEY,
    id_disciplina INT,
    id_professor INT,
    semestre VARCHAR(10) NOT NULL,
    ano INT NOT NULL,
    FOREIGN KEY (id_disciplina) REFERENCES disciplina(id_disciplina),
    FOREIGN KEY (id_professor) REFERENCES professor(id_professor)
);

CREATE TABLE matricula (
    id_matricula INT AUTO_INCREMENT PRIMARY KEY,
    id_aluno INT,
    id_turma INT,
    nota DECIMAL(4,2),
    FOREIGN KEY (id_aluno) REFERENCES aluno(id_aluno),
    FOREIGN KEY (id_turma) REFERENCES turma(id_turma)
);
