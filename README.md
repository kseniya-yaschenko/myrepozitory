# myrepozitory
my first repozitory

CREATE TABLE READERS(
  ID NUMBER PRIMARY KEY,
  NAME VARCHAR(20) NOT NULL,
  DATE_OF_BIRTH DATE NOT NULL,
  SEX VARCHAR(10) NOT NULL,
  subs_num_ID NUMBER NOT NULL
);

INSERT INTO READERS VALUES ('1','Masha', '14.09.2012', 'female','5'); 
INSERT INTO READERS VALUES ('2','Sergey', '18.02.1987', 'male','1'); 
INSERT INTO READERS VALUES ('3','Petya', '09.10.1995', 'male','6'); 
INSERT INTO READERS VALUES ('4','Kolya', '16.03.2001', 'male','2'); 
INSERT INTO READERS VALUES ('5','Vanya', '23.06.1990', 'male','3'); 
INSERT INTO READERS VALUES ('6','Olecya', '03.12.1998', 'female','4'); 


CREATE TABLE GENRE(
  ID NUMBER PRIMARY KEY,
GENRE VARCHAR (30) NOT NULL
);

INSERT INTO GENRE VALUES ('1','detective'); 
INSERT INTO GENRE VALUES ('2','fantasy'); 
INSERT INTO GENRE VALUES ('3','novels'); 
INSERT INTO GENRE VALUES ('4','fairy tales'); 
INSERT INTO GENRE VALUES ('5','scientific literature'); 
INSERT INTO GENRE VALUES ('6','classic'); 

CREATE TABLE author(
  ID NUMBER PRIMARY KEY,
 author VARCHAR(50) NOT NULL
);


INSERT INTO author VALUES ('1','Dan Brown'); 
INSERT INTO author VALUES ('2','Boris Akunin'); 
INSERT INTO author VALUES ('3','Margaret Mitchell'); 
INSERT INTO author VALUES ('4','Colin McCullough'); 
INSERT INTO author VALUES ('5','Veronica Roth'); 
INSERT INTO author VALUES ('6','HG Wells'); 
INSERT INTO author VALUES ('7','Gomer'); 
INSERT INTO author VALUES ('8','Evgeny Vorobev'); 
INSERT INTO author VALUES ('9','Andrey Belyanin'); 
INSERT INTO author VALUES ('10','Lev Tolstoy'); 
INSERT INTO author VALUES ('11','Lev Gumilyov'); 
INSERT INTO author VALUES ('12','Laue'); 

CREATE TABLE books(
  ID NUMBER PRIMARY KEY,
 title VARCHAR(50) NOT NULL,
GENRE_ID NUMBER  NOT NULL
FOREIGN KEY (GENRE_ID) REFERENCES GENRE (ID)
);

ALTER TABLE books ADD FOREIGN KEY GENRE_ID REFERENCES GENRE (ID));

ALTER TABLE books ADD AUTOR_ID NUMBER NOT NULL;

INSERT INTO books VALUES ('1','The Da Vinci Code', '1','1'); 
INSERT INTO books VALUES ('2','Azazel', '1','2'); 
INSERT INTO books VALUES ('3','Gone With the Wind', '3','3'); 
INSERT INTO books VALUES ('4','Singing in the thorns', '3','4'); 
INSERT INTO books VALUES ('5','Divergent', '2','5');
INSERT INTO books VALUES ('6','War of the Worlds', '2','6');
INSERT INTO books VALUES ('7','33 heroes', '4','8');
INSERT INTO books VALUES ('8','flying ship', '4','9'); 
INSERT INTO books VALUES ('9','War and Peace', '6','10');
INSERT INTO books VALUES ('10','Odyssey', '6','7');
INSERT INTO books VALUES ('11','Entogenesis and biosphere of the earth', '5','11');
INSERT INTO books VALUES ('12','History of physics', '5','12');

ALTER TABLE books ADD FOREIGN KEY AUTHOR_ID REFERENCES AUTHOR (ID));

CREATE TABLE subscription (
  ID NUMBER PRIMARY KEY,
BOOK_ID NUMBER  NOT NULL,
date_of_issue DATE NOT NULL);


INSERT INTO subscription VALUES ('1','3','17.04.2019'); 
INSERT INTO subscription VALUES ('2','5','18.04.2019'); 
INSERT INTO subscription VALUES ('3','7','19.04.2019'); 
INSERT INTO subscription VALUES ('4','8','20.04.2019'); 
INSERT INTO subscription VALUES ('5','1','21.04.2019'); 
INSERT INTO subscription VALUES ('6','2','22.04.2019');
INSERT INTO subscription VALUES ('7','11','21.04.2019');  


ALTER TABLE subscription ADD FOREIGN KEY BOOK_ID REFERENCES BOOKS (ID));

ALTER TABLE readers ADD FOREIGN KEY subs_num_ID REFERENCES subscription (ID));

UPDATE READERS SET NAME =  Ivan WHERE ID = 2;


SELECT t.title as 'title',g.genre as 'genre' 
FROM books t, genre g
WHERE g.id = t.genre_id;

SELECT t.title as 'title',s.date_of_issue as 'date_of_issue', r.name as 'name'
FROM books t, subscription s, readers r
WHERE t.id = s.book_id and s.id = r.subs_num_id;

SELECT r.NAME as 'name', s.date_of_issue as 'date_of_issue'
FROM readers r, subscription s
WHERE s.id = r.subs_num_id AND g.genre_id=(SELECT id FROM genre where genre ='detective');


DElete from books where title = Azaael;

ALTER TABLE books DROP CONSTRAINT GENRE_ID;
ALTER TABLE books DROP CONSTRAINT AUTHOR_ID;
ALTER TABLE subscription DROP CONSTRAINT BOOK_ID;
ALTER TABLE readers DROP CONSTRAINT subs_num_ID;

DROP TABLE READERS;
DROP TABLE subscription;
DROP TABLE books;
DROP TABLE AUTHOR;
DROP TABLE READERS;
