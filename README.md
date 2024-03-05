
# Administrador de Banco de Dados
Curso no Senai de Administrador de Banco de Dados

[Página do curso](https://sistemafibra.org.br/senai/custom/inovatech/index.php#)
 | [Código das Aulas](https://drive.google.com/drive/folders/1SBetwEQKxlasAd-UDQrnkttZgf4RRoEI)

## Aula 001 - 📅 20/02/2024 - Ter

- [Livro do curso](https://estantedelivros.senai.br/share/1XIATE6Jfo0MXUS7r8a9CGqL323ctB5-X)

-

## Aula 002 - 📅 21/02/2024 - Qua
## Aula 003 - 📅 22/02/2024 - Qui
## Aula 004 - 📅 23/02/2024 - Sex
## Aula 005 - 📅 26/02/2024 - Seg
## Aula 006 - 📅 27/02/2024 - Ter
## Aula 007 - 📅 29/02/2024 - Qua
## Aula 008 - 📅 01/03/2024 - Qui

--- Criação do banco de dados 
create DATABASE	escola;
--------------------------------------------------------------

--- Ligação com o banco de dados 
use escola;

--------------------------------------------------------------
--- Criação de tabelas 
--------------------------------------------------------------

create table turma(
id_turma int auto_increment primary key,
cod_turma varchar (11),
turno varchar (50),
data_inicio date,
data_final date
);
create table curso(
id_curso int auto_increment primary key,
nome varchar (100),
modalidade varchar (45),
carga_horaria int,
codigo_turma varchar (20)
);
create table disciplina(
id_disciplina int auto_increment primary key,
nome varchar (50),
carga_horaria int
);
create table sala(
id_sala int auto_increment primary key,
numero int,
qt_max_aluno int
);
create table sexo(
id_sexo int auto_increment primary key,
sexo varchar (45)
);

--------------------------------------------------------------
--- + foreing 
--------------------------------------------------------------

create table aluno(
id_aluno int auto_increment primary key,
nome varchar (200) not null,
cpf varchar (20) not null unique, 
rg varchar (15) not null unique,
data_nascimento date,
etnia varchar (60),
telefone varchar (20),
nacionalidade varchar (50),
uf varchar (2),
id_sexo int,
foreign key (id_sexo) references sexo(id_sexo)
);
create table professor(
id_professor int auto_increment primary key,
nome varchar (200) not null,
cpf varchar (20) not null unique, 
rg varchar (15) not null unique,
email varchar (250),
telefone varchar (20),
matricula varchar (15),
lotacao varchar (45),
id_sexo int,
foreign key (id_sexo) references sexo(id_sexo)
);
create table login(
senha varchar (45),
id_aluno int,
id_professor int,
foreign key (id_aluno) references aluno(id_aluno),
foreign key (id_professor) references professor(id_professor)
);

--------------------------------------------------------------
--- foreing 
--------------------------------------------------------------

create table aluno_has_turma(
id_aluno int,
id_turma int,
foreign key (id_aluno) references aluno(id_aluno),
foreign key (id_turma) references turma(id_turma)
);
create table professor_has_turma(
id_professor int,
id_turma int,
foreign key (id_professor) references professor(id_professor),
foreign key (id_turma) references turma(id_turma)
);
create table turma_has_curso(
id_turma int,
id_curso int,
foreign key (id_turma) references turma(id_turma),
foreign key (id_curso) references curso(id_curso)
);
create table sala_has_turma(
id_sala int,
id_turma int,
foreign key (id_sala) references sala(id_sala),
foreign key (id_turma) references turma(id_turma)
);
create table curso_has_disciplina(
id_curso int,
id_disciplina int,
foreign key (id_curso) references curso(id_curso),
foreign key (id_disciplina) references disciplina(id_disciplina)
);


--------------------------------------------------------------
--- insert // SEXO
--------------------------------------------------------------

insert into sexo(sexo) values("M"),("F");

update aluno set id_sexo = 2 where id_aluno = 12;

--------------------------------------------------------------
--- insert // ALUNO
--------------------------------------------------------------

insert into aluno(nome,cpf,rg,data_nascimento,etnia,telefone,nacionalidade,uf,id_sexo) 
values ("Diego de Araujo Lima", "024.936.901-09","110135","1991-03-24","Preto", "61 991331180","Brasileiro","DF","1");

insert into aluno(nome,cpf,rg,data_nascimento,etnia,telefone,nacionalidade,uf,id_sexo) 
values ("Bruno Lima","024.906.001-00","111584","1991-04-24","Preto","61991331180","Brasileiro","DF","1"),
("Joao Paulo","024.906.001-01","118214","1991-04-12","Branco","61991331181","Brasileiro","RJ","1"),
("Fernada Lima","024.906.001-02","189684","1981-03-01","Pardo","61991331182","Brasileiro","BA","2"),
("Maria Silva","024.906.001-03","1983284","1991-08-01","Preto","61991331183","Brasileiro","MA","2"),
("Bruna Cardoso","024.906.001-04","18231684","1998-03-01","Branco","61991331184","Brasileiro","CE","1"),
("Joao Moreira","024.906.001-05","1156489","1992-03-01","Pardo","61991331185","Brasileiro","SP","1");


--------------------------------------------------------------
--- insert // PROFESSOR
--------------------------------------------------------------

insert into professor(nome,cpf,rg,email,telefone,matricula,lotacao,id_sexo)
values ("João da Silva","011.111.111-08","123456","joao.silva@gmail.com","619999999","100","Guara","1");

insert into professor(nome,cpf,rg,email,telefone,matricula,lotacao,id_sexo)
values ("Bruna Carol","251.111.111-08","1234357","bruna@gmail.com","619998999","101","Cruzeiro","2"),
("Bernado Silva","331.111.111-08","123457","Bernardo@gmail.com","6191298999","102","Samambaia","1"),
("Maria Lima","44.111.111-08","1234578","maria@gmail.com","619678999","103","Asa Sul","2"),
("Fernando Costa","255.111.111-08","1253457","fernando@gmail.com","6199678999","104","Sobradinh","1"),
("Ariel Melo","251.166.111-08","1234574","ariel@gmail.com","619998999","105","SIG","1"),
("Pedro Joao","251.188.111-08","12345718","pedro@gmail.com","6196798999","106","Asa Norte","1"),
("Denise Maria","251.911.111-08","1234517","denise@gmail.com","6199967899","107","Sudoeste","2");

--------------------------------------------------------------
--- insert // LOGIN - --professor
--------------------------------------------------------------
select * from login;

select * from login;
insert into login(senha,id_professor)
values ("12345",1),("124485",9),("12345",10),("1234aq5",11),("12q335",12),("12345",13),("1234qe5",14),("12345eer",15);

alter table login add column id_login int auto_increment primary key; 

--------------------------------------------------------------
--- insert // LOGIN - --aluno
--------------------------------------------------------------

select * from aluno;
insert into login(senha,id_aluno)
values ("fd12345",1),("124fd485",8),("1rt2345",9),("1234ewraq5",10),("12q3werw5",11),("123wqe45",12),("qwe1234qe5",13);

--------------------------------------------------------------
--- insert // CURSO
--------------------------------------------------------------

select * from curso;
insert into curso(nome,modalidade,carga_horaria,codigo_turma)
values ("Publicidade e Propaganda","EAD","2000","PB-001"),
("Administrador de Banco de Dados","Presencial","240","ADMB-001"),
("Administração","Semi-Presencial","1240","ADM-001"),
("Direito","Presencial","2240","DIR-001");

--------------------------------------------------------------
--- insert // DISCIPLINA 
-------------------------------------------------------------

select * from disciplina;
insert into disciplina(nome,carga_horaria)
values ("Fotografia","100"),
("MySQL","30"),
("TGA","50"),
("Direito da Familia","50");

--------------------------------------------------------------
--- insert // SALA
-------------------------------------------------------------

select * from sala;
insert into sala(numero,qt_max_aluno)
values ("301","30"),
("302","30"),
("303","50"),
("304","10"),
("305","20");

--------------------------------------------------------------
--- insert // TURMA
-------------------------------------------------------------

select * from turma;
insert into turma(cod_turma,turno,data_inicio,data_final)
values ("001-A","Matutino","2024-03-01","2025-03-01"),
("002-B","Vespertino","2024-03-01","2026-03-01"),
("001-C","Noturno","2024-03-01","2025-12-01"),
("005-F","Matutino","2024-12-01","2025-12-01");

--------------------------------------------------------------
--- insert // PROFESSOR_HAS_TURMA
-------------------------------------------------------------

select * from professor;
select * from turma;
select * from professor_has_turma;

insert into professor_has_turma(id_professor,id_turma)
values (1,1),(1,2),(1,4);

insert into professor_has_turma(id_professor,id_turma)
values (10,2),(10,4);

--------------------------------------------------------------
--- insert // CURSO_HAS_DISCIPLINA
-------------------------------------------------------------

select * from curso;
select * from disciplina;
select * from curso_has_disciplina;

insert into curso_has_disciplina(id_curso,id_disciplina)
values (1,1);

insert into curso_has_disciplina(id_curso,id_disciplina)
values (2,2);

insert into curso_has_disciplina(id_curso,id_disciplina)
values (3,3);

insert into curso_has_disciplina(id_curso,id_disciplina)
values (4,4);

--------------------------------------------------------------
--- insert // TURMA_HAS_CURSO
-------------------------------------------------------------

select * from turma;
select * from curso;
select * from turma_has_curso;

insert into turma_has_curso(id_turma,id_curso)
values (1,1);

insert into turma_has_curso(id_turma,id_curso)
values (2,2);

insert into turma_has_curso(id_turma,id_curso)
values (3,3);

insert into turma_has_curso(id_turma,id_curso)
values (4,4);

--------------------------------------------------------------
--- insert // ALUNO_HAS_TURMA
-------------------------------------------------------------

select * from aluno;
select * from turma;
select * from aluno_has_turma;

insert into aluno_has_turma(id_aluno,id_turma)
values (1,1);

insert into aluno_has_turma(id_aluno,id_turma)
values (8,2);

insert into aluno_has_turma(id_aluno,id_turma)
values (9,3);

insert into aluno_has_turma(id_aluno,id_turma)
values (10,4);

insert into aluno_has_turma(id_aluno,id_turma)
values (11,1);

insert into aluno_has_turma(id_aluno,id_turma)
values (12,2);

insert into aluno_has_turma(id_aluno,id_turma)
values (13,3);


--------------------------------------------------------------
--- inner join // TABELA ALUNO + SEXO
-------------------------------------------------------------

select nome,cpf,rg,data_nascimento,etnia,telefone,nacionalidade,uf,s.sexo from
aluno a 
inner join sexo s
on s.id_sexo = a.id_sexo;

select * from aluno;

--------------------------------------------------------------
--- inner join // ALUNO + TURMA
-------------------------------------------------------------

SELECT a.nome,t.id_turma,m.nome
FROM aluno a
INNER JOIN aluno_has_turma t ON t.id_turma = t.id_turma,
INNER JOIN turma m on m.nome = m.nome

select * from aluno_has_turma;




select
 a.nome,
 a.cpf,
 a.rg,
 s.sexo,
 t.cod_turma,
 t.turno,
 t.data_inicio,
 t.data_final,
 p.nome,
 p.matricula
from aluno a
inner join sexo s on s.id_sexo = a.id_sexo
inner join aluno_has_turma at on at.id_aluno = a.id_aluno
inner join turma t on t.id_turma = at.id_turma
inner join professor_has_turma pt on pt.id_turma = t.id_turma
inner join professor p on p.id_professor = pt.id_professor;

## Aula 009 - 📅 04/03/2024 - Sex
## Aula 010 - 📅 05/03/2024 - Seg
## Aula 011 - 📅 06/03/2024 - Ter