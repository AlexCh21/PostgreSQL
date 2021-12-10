## Проектирование БД. Связи. 3НФ

 Связи
 
```

create table if not exists genre (
	id_genre serial unique,
	name varchar(30) not null unique
);
create table if not exists artist (
	id_artist serial unique,
	name varchar(30) unique
);
create table if not exists nickname (
	id_nick serial unique,
	name varchar(30) unique,
	id_artist integer references artist(id_artist)
);
create table if not exists album (
	id_album serial unique,
	name varchar(30) not null,
	release_yaer integer not null,
	id_genre integer references genre(id_genre)
);
create table if not exists track (
	id_track serial unique,
	name varchar(50) not null,
	track_length integer not null,
	id_album integer references album(id_album)
);
create table if not exists collection (
	id_collection serial unique,
	name varchar(50) not null,
	release_yaer integer not null
);
create table if not exists genre_nickname (
	id_genre integer references genre(id_genre),
	id_nick integer references nickname(id_nick),
	constraint gn primary key (id_genre, id_nick)
);
create table if not exists album_nickname (
	id_nick integer references nickname(id_nick),
	id_album integer references album(id_album),
	constraint na primary key (id_nick, id_album)
);
create table if not exists collection_track (
	id serial unique,
	id_collection integer not null references collection(id_collection),
	id_track integer not null references track(id_track),
	constraint ct primary key (id_collection, id_track)
);

```
