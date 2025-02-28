--CREATE DATABASE PROGETTO_S15

USE PROGETTO_S15

CREATE TABLE ANAGRAFICA (
idanagrafica UNIQUEIDENTIFIER NOT NULL PRIMARY KEY,
Cognome NVARCHAR(40) NOT NULL,
Nome NVARCHAR(40) NOT NULL,
Indirizzo NVARCHAR(100) NOT NULL,
Citta NVARCHAR(50) NOT NULL,
CAP NVARCHAR(5) NOT NULL,
Cod_Fisc NVARCHAR(16) NOT NULL
)

CREATE TABLE VIOLAZIONE (
idviolazione UNIQUEIDENTIFIER NOT NULL PRIMARY KEY,
descrizione NVARCHAR(300) NOT NULL
)

CREATE TABLE VERBALE(
idverbale INT NOT NULL,
DataViolazione DATETIME NOT NULL,
IndirizzoViolazione NVARCHAR(100) NOT NULL,
Nominativo_Agente NVARCHAR(40) NOT NULL,
DataTrascrizioneVerbale DATETIME NOT NULL,
Importo MONEY NOT NULL,
DecurtamentoPunti INT,
idanagrafica UNIQUEIDENTIFIER NOT NULL,
idviolazione UNIQUEIDENTIFIER NOT NULL,
CONSTRAINT FK_ID_ANAGRAFICA FOREIGN KEY(idanagrafica) REFERENCES ANAGRAFICA(idanagrafica),
CONSTRAINT FK_ID_VIOLAZIONE FOREIGN KEY(idviolazione) REFERENCES VIOLAZIONE(idviolazione),
CONSTRAINT PK_VERBALE PRIMARY KEY (idverbale, idviolazione, idanagrafica)
)

--POPOLAMENTO ANAGRAFICA
INSERT INTO ANAGRAFICA (idanagrafica, Cognome, Nome, Indirizzo, Citta, CAP, Cod_Fisc)
VALUES
  (NEWID(), 'Rossi', 'Mario', 'Via Roma 12', 'Milano', '20100', 'RSSMRA80A01H501Z'),
  (NEWID(), 'Bianchi', 'Giulia', 'Piazza Garibaldi 3', 'Roma', '00100', 'BNCGLL85C55Z404P'),
  (NEWID(), 'Verdi', 'Luca', 'Via Milano 45', 'Napoli', '80100', 'VRDLCA70A01F839Y'),
  (NEWID(), 'Neri', 'Laura', 'Corso Italia 67', 'Firenze', '50100', 'NRLLRA60A01A001X'),
  (NEWID(), 'Gialli', 'Andrea', 'Viale delle Libertà 89', 'Torino', '10100', 'GLANDR80B01H501T'),
  (NEWID(), 'Blu', 'Carla', 'Strada Provinciale 12', 'Bologna', '40100', 'BLUCRL65C52E123G'),
  (NEWID(), 'Rossi', 'Giovanni', 'Via Parini 23', 'Genova', '16100', 'RSSGNN76M01F205F'),
  (NEWID(), 'Lombardi', 'Francesca', 'Via delle Rose 8', 'Venezia', '30100', 'LMBFNC81B41Z404F'),
  (NEWID(), 'Russo', 'Paolo', 'Via Dante 34', 'Catania', '95100', 'RSSPLS75D15C351L'),
  (NEWID(), 'Ferrari', 'Alessandro', 'Viale dei Tigli 56', 'Padova', '35100', 'FRRLSS85D03F205P'),
  (NEWID(), 'Mancini', 'Simona', 'Via Milano 10', 'Bari', '70100', 'MNCSSM72S49C351J'),
  (NEWID(), 'Costa', 'Antonio', 'Largo Adua 2', 'Lecce', '73100', 'CSTNTN77A01H501W'),
  (NEWID(), 'Cattaneo', 'Luca', 'Piazza del Popolo 1', 'Perugia', '06100', 'CTNLCA65C12C351N'),
  (NEWID(), 'De Luca', 'Sofia', 'Via dei Mille 45', 'Reggio Calabria', '89100', 'DLCSFA91L51L219P'),
  (NEWID(), 'Martini', 'Francesco', 'Viale XX Settembre 7', 'Salerno', '84100', 'MRTFNC67C12F839X'),
  (NEWID(), 'Monti', 'Giorgio', 'Corso Vittorio Emanuele 11', 'Messina', '98100', 'MNTGRG63D10C351A'),
  (NEWID(), 'Fontana', 'Valentina', 'Via delle Viole 6', 'Trieste', '34100', 'FNTLVT70A41Z404F'),
  (NEWID(), 'Barbieri', 'Giuseppe', 'Via Santa Maria 14', 'Cagliari', '09100', 'BRBGPP88B10D123X'),
  (NEWID(), 'Giordano', 'Riccardo', 'Piazza del Duomo 22', 'Pisa', '56100', 'GRDRRD89M01F205X');

--POPOLAMENTO VIOLAZIONI
INSERT INTO VIOLAZIONE (idviolazione, descrizione)
VALUES
  (NEWID(), 'Superamento dei limiti di velocità'),
  (NEWID(), 'Guida senza cintura di sicurezza'),
  (NEWID(), 'Passaggio con semaforo rosso'),
  (NEWID(), 'Sosta in area riservata ai disabili'),
  (NEWID(), 'Mancato uso del casco per motociclisti'),
  (NEWID(), 'Guida in stato di ebbrezza'),
  (NEWID(), 'Utilizzo del cellulare durante la guida'),
  (NEWID(), 'Sorpasso in zona vietata'),
  (NEWID(), 'Circolazione contromano'),
  (NEWID(), 'Guida senza patente'),
  (NEWID(), 'Eccesso di velocità in zona scolastica'),
  (NEWID(), 'Passaggio a livello senza fermarsi'),
  (NEWID(), 'Mancato rispetto delle distanze di sicurezza'),
  (NEWID(), 'Uso improprio dei fari abbaglianti'),
  (NEWID(), 'Sosta su strisce pedonali'),
  (NEWID(), 'Guida sotto l’effetto di sostanze stupefacenti'),
  (NEWID(), 'Violazione della segnaletica stradale'),
  (NEWID(), 'Rallentamento in autostrada senza giustificato motivo'),
  (NEWID(), 'Sosta in divieto di sosta'),
  (NEWID(), 'Mancato utilizzo del triangolo di emergenza');

--POPOLAMENTO VERBALI
INSERT INTO VERBALE (idverbale, DataViolazione, IndirizzoViolazione, Nominativo_Agente, DataTrascrizioneVerbale, Importo, DecurtamentoPunti, idanagrafica, idviolazione)
VALUES
(1, '2025-01-02 12:00:00', 'Via Roma 12', 'Agente Rossi', '2025-01-02 12:30:00', 150.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Rossi' AND Nome = 'Mario'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Superamento dei limiti di velocità')),
(2, '2025-02-02 14:00:00', 'Piazza Garibaldi 3', 'Agente Bianchi', '2025-02-02 14:30:00', 100.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Bianchi' AND Nome = 'Giulia'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza')),
(3, '2025-03-02 08:00:00', 'Via Milano 45', 'Agente Verdi', '2025-03-02 08:30:00', 120.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Verdi' AND Nome = 'Luca'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Passaggio con semaforo rosso')),
(4, '2025-04-02 10:00:00', 'Corso Italia 67', 'Agente Neri', '2025-04-02 10:30:00', 80.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Neri' AND Nome = 'Laura'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Sosta in area riservata ai disabili')),
(5, '2025-05-02 09:00:00', 'Viale delle Libertà 89', 'Agente Gialli', '2025-05-02 09:30:00', 200.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Gialli' AND Nome = 'Andrea'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Mancato uso del casco per motociclisti')),
(6, '2025-06-02 11:00:00', 'Strada Provinciale 12', 'Agente Blu', '2025-06-02 11:30:00', 300.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Blu' AND Nome = 'Carla'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida in stato di ebbrezza')),
(7, '2025-07-02 13:00:00', 'Via Parini 23', 'Agente Rossi', '2025-07-02 13:30:00', 100.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Rossi' AND Nome = 'Giovanni'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Utilizzo del cellulare durante la guida')),
(8, '2025-08-02 15:00:00', 'Piazza Garibaldi 3', 'Agente Lombardi', '2025-08-02 15:30:00', 150.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Lombardi' AND Nome = 'Francesca'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Sorpasso in zona vietata')),
(9, '2025-09-02 16:00:00', 'Via delle Rose 8', 'Agente Russo', '2025-09-02 16:30:00', 50.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Russo' AND Nome = 'Paolo'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Circolazione contromano')),
(10, '2025-10-02 17:00:00', 'Via Dante 34', 'Agente Ferrari', '2025-10-02 17:30:00', 80.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Ferrari' AND Nome = 'Alessandro'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza patente')),
(11, '2025-11-02 09:00:00', 'Viale dei Tigli 56', 'Agente Mancini', '2025-11-02 09:30:00', 100.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Mancini' AND Nome = 'Simona'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Eccesso di velocità in zona scolastica')),
(12, '2025-12-02 11:00:00', 'Via dei Mille 45', 'Agente Costa', '2025-12-02 11:30:00', 70.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Costa' AND Nome = 'Antonio'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Passaggio a livello senza fermarsi')),
(13, '2025-13-02 13:00:00', 'Via delle Viole 6', 'Agente Cattaneo', '2025-13-02 13:30:00', 60.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Cattaneo' AND Nome = 'Luca'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Mancato rispetto delle distanze di sicurezza')),
(14, '2025-14-02 14:00:00', 'Piazza del Popolo 1', 'Agente De Luca', '2025-14-02 14:30:00', 200.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'De Luca' AND Nome = 'Sofia'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Uso improprio dei fari abbaglianti')),
(15, '2025-15-02 15:00:00', 'Viale XX Settembre 7', 'Agente Martini', '2025-15-02 15:30:00', 250.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Martini' AND Nome = 'Francesco'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Sosta su strisce pedonali')),
(16, '2025-16-02 16:00:00', 'Corso Vittorio Emanuele 11', 'Agente Monti', '2025-16-02 16:30:00', 180.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Monti' AND Nome = 'Giorgio'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida sotto l’effetto di sostanze stupefacenti')),
(17, '2025-17-02 17:00:00', 'Via Roma 12', 'Agente Fontana', '2025-17-02 17:30:00', 120.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Fontana' AND Nome = 'Valentina'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Violazione della segnaletica stradale')),
(18, '2025-18-02 08:00:00', 'Via Santa Maria 14', 'Agente Barbieri', '2025-18-02 08:30:00', 130.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Barbieri' AND Nome = 'Giuseppe'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Rallentamento in autostrada senza giustificato motivo')),
(19, '2025-19-02 09:00:00', 'Piazza del Duomo 22', 'Agente Giordano', '2025-19-02 09:30:00', 90.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Giordano' AND Nome = 'Riccardo'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Sosta in divieto di sosta')),
(20, '2025-20-02 10:00:00', 'Via Milano 10', 'Agente Rossi', '2025-20-02 10:30:00', 110.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Rossi' AND Nome = 'Giovanni'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Mancato utilizzo del triangolo di emergenza')),
(1, '2025-01-02 12:00:00', 'Via Roma 12', 'Agente Rossi', '2025-01-02 12:30:00', 150.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Rossi' AND Nome = 'Mario'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida sotto l’effetto di sostanze stupefacenti')),
(2, '2025-02-02 14:00:00', 'Piazza Garibaldi 3', 'Agente Bianchi', '2025-02-02 14:30:00', 100.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Bianchi' AND Nome = 'Giulia'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Sorpasso in zona vietata')),
(3, '2025-03-02 08:00:00', 'Via Milano 45', 'Agente Verdi', '2025-03-02 08:30:00', 120.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Verdi' AND Nome = 'Luca'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza patente')),
(4, '2025-04-02 10:00:00', 'Corso Italia 67', 'Agente Neri', '2025-04-02 10:30:00', 80.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Neri' AND Nome = 'Laura'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Circolazione contromano')),
(6, '2025-06-02 11:00:00', 'Strada Provinciale 12', 'Agente Blu', '2025-06-02 11:30:00', 300.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Blu' AND Nome = 'Carla'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza')),
(7, '2025-07-02 13:00:00', 'Via Parini 23', 'Agente Rossi', '2025-07-02 13:30:00', 100.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Rossi' AND Nome = 'Giovanni'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza')),
(8, '2025-08-02 15:00:00', 'Piazza Garibaldi 3', 'Agente Lombardi', '2025-08-02 15:30:00', 150.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Lombardi' AND Nome = 'Francesca'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida in stato di ebbrezza')),
(10, '2025-10-02 17:00:00', 'Via Dante 34', 'Agente Ferrari', '2025-10-02 17:30:00', 80.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Ferrari' AND Nome = 'Alessandro'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida in stato di ebbrezza')),
(11, '2025-11-02 09:00:00', 'Viale dei Tigli 56', 'Agente Mancini', '2025-11-02 09:30:00', 100.00, 2, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Mancini' AND Nome = 'Simona'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza')),
(13, '2025-13-02 13:00:00', 'Via delle Viole 6', 'Agente Cattaneo', '2025-13-02 13:30:00', 60.00, 1, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Cattaneo' AND Nome = 'Luca'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza')),
(14, '2025-14-02 14:00:00', 'Piazza del Popolo 1', 'Agente De Luca', '2025-14-02 14:30:00', 200.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'De Luca' AND Nome = 'Sofia'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza')),
(16, '2025-16-02 16:00:00', 'Corso Vittorio Emanuele 11', 'Agente Monti', '2025-16-02 16:30:00', 180.00, 3, (SELECT idanagrafica FROM ANAGRAFICA WHERE Cognome = 'Monti' AND Nome = 'Giorgio'), (SELECT idviolazione FROM VIOLAZIONE WHERE descrizione = 'Guida senza cintura di sicurezza'));

--QUERY

--1)
SELECT COUNT(*) AS TOT_VERBALI FROM VERBALE;

--2)
SELECT Nome, Cognome, COUNT(idverbale) as TOT_VERBALI FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica GROUP BY ANAGRAFICA.Nome, ANAGRAFICA.Cognome

--3)
SELECT descrizione, COUNT(idverbale) as TOT_VERBALI FROM VERBALE LEFT JOIN VIOLAZIONE ON VERBALE.idviolazione = VIOLAZIONE.idviolazione GROUP BY VIOLAZIONE.descrizione

--4)
SELECT Nome, Cognome, SUM(DecurtamentoPunti) as TOT_PUNTI FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica GROUP BY ANAGRAFICA.Nome, ANAGRAFICA.Cognome

--5)
SELECT Cognome, Nome, DataViolazione, IndirizzoViolazione, Importo, DecurtamentoPunti FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica WHERE Citta = 'Messina'

--6)
SELECT Cognome, Nome, DataViolazione, IndirizzoViolazione, Importo, DecurtamentoPunti FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica WHERE DataViolazione BETWEEN '2025/01/02' AND '2025/04/02'

--7)
SELECT Nome, Cognome, SUM(Importo) as TOT_IMPORTO FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica GROUP BY ANAGRAFICA.Nome, ANAGRAFICA.Cognome

--8)
SELECT * FROM ANAGRAFICA WHERE Citta = 'Napoli'

--9)
SELECT DataViolazione, Importo, DecurtamentoPunti FROM VERBALE WHERE DataViolazione BETWEEN '2025/01/02 00:00:00' AND '2025/01/02 23:59:59';

--10)
SELECT Nominativo_Agente, count(*) FROM VERBALE GROUP BY Nominativo_Agente

--11)
SELECT Cognome, Nome, DataViolazione, IndirizzoViolazione, Importo, DecurtamentoPunti FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica WHERE DecurtamentoPunti > 2

--12)
SELECT Cognome, Nome, DataViolazione, IndirizzoViolazione, Importo, DecurtamentoPunti FROM ANAGRAFICA INNER JOIN VERBALE ON ANAGRAFICA.idanagrafica = VERBALE.idanagrafica WHERE Importo > 200

--FINE PROGETTO BASE

--QUERY EXTRA

--13) Numero di verbali e importo totale delle multe emesse per ogni agente di polizia
SELECT Nominativo_Agente, COUNT(*) as TOT_VERBALI, SUM(Importo) as TOT_IMPORTO FROM VERBALE GROUP BY Nominativo_Agente

--14) Media degli importi delle multe per tipo di violazione
SELECT descrizione, AVG(Importo) as AVG_IMPORTO FROM VIOLAZIONE LEFT JOIN VERBALE ON VERBALE.idviolazione = VIOLAZIONE.idviolazione GROUP BY descrizione

--EXTRA FINITI