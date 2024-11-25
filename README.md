# Comentarios
Scripts SQL para a criação e manipulação de um banco de dados de Comentarios e Likes.
Comentarios.sql
CREATE SCHEMA IF NOT EXISTS Comentario DEFAULT CHARACTER SET utf8;
use Comentario;

CREATE TABLE IF NOT EXISTS Projetos (
    id integer not null,
    titulo VARCHAR(255) ,
    Data date,
    ulr VARCHAR(100) ,
    primary key (id)
    ) ENGINE = InnoDB;
    
    select * from Projetos;
    
    CREATE TABLE IF NOT EXISTS Usuario (
    id integer not null,
    nome VARCHAR(45) not null ,
    email VARCHAR(45) not null ,
    senha varchar (45) not null,
    primary key (id)
    ) ENGINE = InnoDB;
    
    select * from Usuario;
    
    CREATE TABLE IF NOT EXISTS Comentarios (
    id integer not null,
    comentario text not null,
    data date not null,
	id_Usuario int,
    id_Projetos int,
	foreign key (id_Projetos) references Projetos(id),
    foreign key (id_Usuario) references Usuario(id),
    primary key (id)
    ) ENGINE = InnoDB;
    
	CREATE TABLE IF NOT EXISTS LikesporProjeto (
	id_Usuario int not null,
    id_Projetos int not null,
	foreign key (id_Projetos) references Projetos(id),
    foreign key (id_Usuario) references Usuario(id),
    primary key (id_Usuario, id_Projetos)
    ) ENGINE = InnoDB;

	CREATE TABLE IF NOT EXISTS LikesporComentario (
	id_Usuario int not null,
    id_Comentario int not null,
	foreign key (id_Comentario) references Comentario(id),
    foreign key (id_Usuario) references Usuario(id),
    primary key (id_Usuario, id_Comentario)
    ) ENGINE = InnoDB;
    
     INSERT INTO Projetos VALUES (1,'aplicação c#', '2018-04-01','www.aplicacaosharp.com.br');
     INSERT INTO Projetos VALUES (2,'aplicação ionic', '2018-05-07','www.aplicacaoionic.com.br');
     INSERT INTO Projetos VALUES (3,'aplicação Phyton', '2018-08-05','www.aplicacaophyton.com.br');
     
     INSERT INTO Usuario VALUES (1,'Paola Carvalho', 'paola@gmail.com','pinoqu1o');
     INSERT INTO Usuario VALUES (2,'Julia Santiago', 'julia@gmail.com','js90');
     INSERT INTO Usuario VALUES (3,'Kairo Goulart', 'kairo@gmail.com','l31t04');
     INSERT INTO Usuario VALUES (4,'Lucas Jordão', 'Lucas@gmail.com','j0ed40');
     
     INSERT INTO Comentarios VALUES (1,'Acertaram muito com essa liguagem', '2018-05-01',1,2);
	 INSERT INTO Comentarios VALUES (2,'Um jeito muito facil de ensinar', '2018-07-06',4,3);
	 INSERT INTO Comentarios VALUES (3,'Aprendi muito nessas aulas', '2018-04-18',2,3);
	 INSERT INTO Comentarios VALUES (4,'Adorei aprender c#', '2018-07-26',1,1);
	 INSERT INTO Comentarios VALUES (5,'Muito maneiro esse framework', '2019-10-06',3,2);
	 INSERT INTO Comentarios VALUES (6,'Simples e pratico, como eu queria', '2019-01-30',2,1);
	 INSERT INTO Comentarios VALUES (7,'Parabéns pelo otimo projeto', '2018-10-28',3,3);
     
    INSERT INTO LikesporProjeto VALUES (2,3);
    INSERT INTO LikesporProjeto VALUES (1,2);
    INSERT INTO LikesporProjeto VALUES (1,1);
    INSERT INTO LikesporProjeto VALUES (4,3);
    INSERT INTO LikesporProjeto VALUES (3,1);
    INSERT INTO LikesporProjeto VALUES (3,3);
    INSERT INTO LikesporProjeto VALUES (4,1);
    
    INSERT INTO LikesporComentario VALUES (1,7);
    INSERT INTO LikesporComentario VALUES (2,7);
    INSERT INTO LikesporComentario VALUES (4,7);
    
    select P.titulo, (select count(C.id_Projetos)
    from Comentarios C 
    where C.id_Projetos = P.id) Quantidade_Comentario
    from Projetos P
    group by P.id;
