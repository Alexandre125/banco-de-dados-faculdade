# banco-de-dados-faculdade

create database db_Faculdade;
use db_Faculdade;

CREATE TABLE tbl_Departamento (
CodDepartamento SMALLINT PRIMARY KEY AUTO_INCREMENT,
NomeDepartamento VARCHAR(50) NOT NULL
);
DESCRIBE tbl_Departamento;

CREATE TABLE tbl_Professor (
CodProfessor SMALLINT PRIMARY KEY NOT NULL,
NomeProfessor VARCHAR(80) NOT NULL,
CodDepartamento SMALLINT NOT NULL,
CONSTRAINT fk_CodDepartamento FOREIGN KEY (CodDepartamento) REFERENCES tbl_Departamento (CodDepartamento) ON DELETE CASCADE
);
DESCRIBE tbl_Professor;

CREATE TABLE tbl_Curso (
CodCurso SMALLINT PRIMARY KEY NOT NULL,
NomeCurso VARCHAR(20) NOT NULL,
CodDepartamento SMALLINT NOT NULL,
CONSTRAINT fk_cod_departamento FOREIGN KEY (CodDepartamento) REFERENCES tbl_Departamento (CodDepartamento) ON DELETE CASCADE
);
DESCRIBE tbl_Curso;

CREATE TABLE tbl_Turmas (
Cod_turma SMALLINT PRIMARY key NOT NULL AUTO_INCREMENT,
Numer_alunos SMALLINT NOT NULL,
CodDepartamento SMALLINT NOT NULL,
CodCurso SMALLINT NOT NULL,
CONSTRAINT  fk_CODDepartament FOREIGN KEY (CodDepartamento) REFERENCES tbl_Departamento (CodDepartamento) ON DELETE CASCADE,
CONSTRAINT fk_CODCurso_turmas FOREIGN KEY (CodCurso) REFERENCES tbl_Curso (CodCurso) ON DELETE CASCADE 
);

DESCRIBE tbl_Turmas;

CREATE TABLE tbl_Disciplina (
CodDisciplina smallint primary key not null,
NomeDisciplina varchar (25) not null,
CodDepartamento SMALLINT NOT NULL,
constraint fk_CodDep foreign key (CodDepartamento) references tbl_Departamento (CodDepartamento) ON DELETE CASCADE
);
DESCRIBE tbl_Disciplina;

CREATE TABLE tbl_Prof_Disc (
CodProfessor SMALLINT NOT NULL,
CodDisciplina SMALLINT NOT NULL,
CONSTRAINT pk_codProf_Disc PRIMARY KEY (CodProfessor, CodDisciplina),
CONSTRAINT fk_codProf FOREIGN KEY (CodProfessor) REFERENCES tbl_Professor (CodProfessor),
CONSTRAINT fk_codDisc FOREIGN KEY (CodDisciplina) REFERENCES tbl_Disciplina (CodDisciplina)
);
DESCRIBE tbl_Prof_Disc;

CREATE TABLE tbl_curso_disciplina (
CodDisciplina smallint not null,
CodCurso smallint not null,
constraint fk_C_disciplina foreign key ( CodDisciplina ) references tbl_disciplina ( CodDisciplina ) on delete cascade,
constraint fk_C_curso foreign key ( CodCurso ) references tbl_curso ( CodCurso ) on delete cascade
);
describe tbl_curso_disciplina;

create table tbl_Alunos (
IdAluno smallint not null auto_increment,
NomeAluno varchar(20) not null,
SobrenomeAluno varchar(60) not null,
CodDisciplina smallint not null,
constraint pk_id_aluno primary key (IdAluno),
constraint fk_coddisciplina foreign key (CodDisciplina) references tbl_Disciplina (CodDisciplina) on delete cascade
);
describe tbl_Alunos;

create table tbl_EnderecoAluno (
CodEndereco smallint not null auto_increment,
IdAluno smallint not null,
NomeRua varchar(70) not null,
NomeBairro varchar(30) not null,
NomeCidade varchar(30) not null,
NumApto smallint,
NumCasa smallint,
constraint pk_id_endereco primary key (CodEndereco),
constraint fk_id_alunos foreign key (IdAluno) references tbl_Alunos (IdAluno) on delete cascade
);
describe tbl_EnderecoAluno;

create table tbl_AlunoDisciplina (
IdAluno smallint not null,
CodDisciplina smallint not null,
constraint fk_C_Disciplin foreign key (CodDisciplina) references tbl_Disciplina (CodDisciplina) on delete cascade,
constraint fk_Id_Aluno foreign key (IdAluno) references tbl_Alunos (IdAluno) on delete cascade
);
describe tbl_AlunoDisciplina;

CREATE TABLE tbl_historicoEscolar (
Cod_historico SMALLINT PRIMARY KEY NOT NULL,
data_inicio DATE NOT NULL,
data_final DATE NOT NULL,
IdAluno smallint NOT NULL,
CONSTRAINT fk_IdAluno  FOREIGN KEY (IdAluno) REFERENCES tbl_Alunos (IdAluno) ON DELETE CASCADE 
);
describe tbl_historicoEscolar;

create table tbl_DisciplinaHistorico (
 Cod_historico smallint not null,
CodDisciplina smallint not null,
constraint fk_C_Discipli foreign key (CodDisciplina) references tbl_Disciplina (CodDisciplina) on delete cascade,
constraint fk_C_historico foreign key (Cod_historico) references  tbl_historicoEscolar (Cod_historico) on delete cascade
);
describe tbl_DisciplinaHistorico;





Select colunas
from tabela1
[inner] join tabela2
on tabela1.coluna=tabela2.coluna;

[inner] join tabelaN
on tabela1.coluna=tabelaN.coluna;

where condiçoes_filtragem
