
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

## Проектирование БД. Связи. 3НФ

 Связи
 
```

create table if not exists Collections (
	id_collection integer unique,
	Collection_name varchar(80) not null,
	Release_year integer check(Release_year > 1970)
);

create table if not exists Genre_Nickname (
	id serial primary key,
	id_genre integer not null references Genres(id_genre),
	id_nick integer not null references Nickname(id_nick),
	constraint gn primary key (id_genre, id_nick)
);

create table if not exists Nickname_Album (
	id serial primary key,
	id_album integer not null references Album(id_album),
	id_nick integer not null references Nickname(id_nick),
	constraint na primary key (id_album, id_nick)
);

create table if not exists Collections_Tracks (
	id serial primary key,
	id_collection integer not null references Collections(id_collection),
	id_track integer not null references Track(id_track),
	constraint ct primary key (id_collection, id_track)
);

```
