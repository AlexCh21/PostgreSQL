
### Домашнее задание 
## Работа с PostgreSQL. Создание БД

 Создание БД
 
```

create table if not exists Genres (
	id_genre serial primary key,
	Genre_name varchar(30) unique
);
create table if not exists Nickname (
	id_nick serial primary key,
	Name varchar(50) unique,
	id_genre integer references Genres(id_genre)
);
create table if not exists Artists (
	id_artist serial primary key,
	Name varchar(50) NOT NULL unique,
	id_nick integer references Nickname(id_nick)
);
create table if not exists Album (
	id_album serial primary key,
	Album_name varchar(50) not null,
	Release_year integer check(Release_year > 1970),
	id_nick integer references Nickname(id_nick)
);
create table if not exists Track (
	id_track serial primary key,
	Track_name varchar(50) not null,
	Track_length integer not null,
	id_album integer references Album(id_album)
);

```

