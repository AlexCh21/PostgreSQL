## Проектирование БД. Связи. 3НФ

 Связи
 
```

create table if not exists genre (
	id_genre serial primary key,
	name varchar(30) not null unique
);
create table if not exists nickname (
	id_nick serial unique,
	name varchar(30) not null unique,
	id_genre integer references genre(id_genre),
	constraint an primary key (id_nick, name)
);
create table artist (
	id_artist serial unique,
	nickname varchar(30) not null,
	id_nick integer references nickname(id_nick),
	constraint ag primary key (id_artist, nickname)
);
create table genre_nickname (
	id_nick integer references nickname(id_nick),
	id_genre integer references genre(id_genre),
	constraint ng primary key (id_nick, id_genre)
);
create table album (
	id_album serial unique,
	name text not null,
	release_yaer integer not null,
	constraint ay primary key (id_album, name)
);
create table album_nickname (
	id_album integer references album(id_album),
	id_nick integer references nickname(id_nick),
	id_genre integer references genre(id_genre),
	constraint al primary key (id_album, id_nick)
);
	create table collection (
	id_collection serial unique,
	name varchar(30) not null,
	release_yaer integer not null,
	constraint cy primary key (id_collection, name)
);
create table track (
	id_track serial unique,
	name varchar(30) not null,
	id_album integer references album(id_album),
	id_collection integer references collection(id_collection),
	track_length integer not null,
	constraint ta primary key (id_track, name)
);
create table if not exists collection_track (
	id serial unique,
	id_collection integer not null references collection(id_collection),
	id_track integer not null references track(id_track),
	id_nick integer references nickname(id_nick),
	constraint ct primary key (id_collection, id_track, id_nick)
);

```
