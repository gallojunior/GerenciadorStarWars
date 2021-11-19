# GerenciadorStarWars
Projeto criado para o bootcamp #2 Everis da DIO


CREATE DATABASE EstrelaDaMorte; <br>
GO

USE EstrelaDaMorte; <br>
GO


CREATE TABLE Planetas( <br>
	IdPlaneta int NOT NULL, <br>
	Nome varchar(50) NOT NULL, <br>
	Rotacao float NOT NULL, <br>
	Orbita float NOT NULL, <br>
	Diametro float NOT NULL, <br>
	Clima varchar(50) NOT NULL, <br>
	Populacao int NOT NULL <br>
) <br>
GO <br>
ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta); <br>
GO


CREATE TABLE Naves( <br>
	IdNave int NOT NULL, <br>
	Nome varchar(100) NOT NULL, <br>
	Modelo varchar(150) NOT NULL, <br>
	Passageiros int NOT NULL, <br>
	Carga float NOT NULL, <br>
	Classe varchar(100) NOT NULL <br>
) <br>
GO <br>
ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave); <br>
GO


CREATE TABLE Pilotos( <br>
	IdPiloto int NOT NULL, <br>
	Nome varchar(200) NOT NULL, <br>
	AnoNascimento varchar(10) NOT NULL, <br>
	IdPlaneta int NOT NULL <br>
) <br>
GO <br>
ALTER TABLE Pilotos ADD CONSTRAINT PK_Pilotos PRIMARY KEY (IdPiloto); <br>
GO <br>
ALTER TABLE Pilotos  ADD  CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY(IdPlaneta) <br>
REFERENCES Planetas (IdPlaneta) <br>
GO <br>
ALTER TABLE Pilotos CHECK CONSTRAINT FK_Pilotos_Planetas <br>
GO


CREATE TABLE PilotosNaves( <br>
	IdPiloto int NOT NULL, <br>
	IdNave int NOT NULL, <br>
	FlagAutorizado bit NOT NULL <br>
) <br>
GO <br>
ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave); <br>
GO <br>
ALTER TABLE PilotosNaves  ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY(IdPiloto) <br>
REFERENCES Pilotos (IdPiloto) <br>
GO <br>
ALTER TABLE PilotosNaves  ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY(IdNave) <br>
REFERENCES Naves (IdNave) <br>
GO <br>
ALTER TABLE PilotosNaves  ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado  DEFAULT (1) FOR FlagAutorizado <br>
GO


CREATE TABLE HistoricoViagens( <br>
	IdNave int NOT NULL, <br>
	IdPiloto int NOT NULL, <br>
	DtSaida datetime NOT NULL, <br>
	DtChegada datetime NULL <br>
) <br>
GO <br>
ALTER TABLE HistoricoViagens  ADD  CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY(IdPiloto, IdNave) <br>
REFERENCES PilotosNaves (IdPiloto, IdNave) <br>
GO <br>
ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves <br>
GO
