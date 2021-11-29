
### Домашнее задание по теме «Работа с PostgreSQL. Создание БД»

 Создание БД
```
create table if not exists Genres (
	id_genre serial primary key,
	Название_жанра varchar(30) unique
);
create table if not exists Nickname (
	id_nick serial primary key,
	Name varchar(50) unique,
	id_genre integer references Genres(id_genre)
);
create table if not exists Artists (
	id_artist serial primary key,
	Имя varchar(50) NOT NULL unique,
	id_nick integer references Nickname(id_nick)
);
create table if not exists Album (
	id_album serial primary key,
	Название_альбома varchar(50) not null,
	Год_выпуска integer check(Год_выпуска > 1990),
	id_nick integer references Nickname(id_nick)
);
create table if not exists Track (
	id_track serial primary key,
	Название_трека varchar(50) not null,
	Длительность VARCHAR(10) not null,
	id_album integer references Album(id_album)
);
```