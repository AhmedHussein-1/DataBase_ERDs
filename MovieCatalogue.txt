drop database if exists MovieCatalogue;

create database MovieCatalogue;

use MovieCatalogue;

-- tables

create table if not exists `Movie`  (
	MovieID int not null primary key auto_increment,
	Title char(128) not null,
    ReleaseDate date null,
	GenreID int not null,
    DirectorID int not null,
    RatingID int not null
	
)engine=InnoDB;

create table if not exists `Genre`  (
	GenreID int not null primary key auto_increment,
	GenreName varchar(30) not null
);

create table if not exists `Director`  (
	DirectorID int primary key auto_increment,
    FirstName varchar(30) not null,
	LastName varchar(30) not null,
	BirthDate date null
);

create table if not exists `Rating` (
	RatingID int not null primary key auto_increment,
	RatingName char(5)not null
    
);

create table if not exists `Actor` (
	ActorID int not null primary key auto_increment,
    FirstName varchar(30) not null,
	LastName varchar(30) not null,
	BirthDate date null
);

create table if not exists `CastMember`  (
	CastMemberID int not null primary key auto_increment,
	Role varchar(50) not null,
    ActorID int not null,
    MovieID int not null
);



alter table `Movie`
	add constraint `fk_Movie_GenreID` 
    foreign key(`GenreID`) 
    references Genre(`GenreID`) on delete no action;
    
alter table `Movie` 
	add constraint `fk_Movie_DirectorID` 
	foreign key(`DirectorID`)
    references Director(`DirectorID`) on delete no action;
    
alter table `Movie`
	add constraint `fk_Movie_RatingID`
    foreign key(`RatingID`) 
    references Rating(`RatingID`) on delete no action;

alter table `CastMember`
	add constraint `fk_CastMembers_ActorID` 
    foreign key(`ActorID`)
    references Actor(`ActorID`) on delete no action;
	
alter table `CastMember`
	add constraint `fk_CastMembers_MovieID` 
    foreign key(`MovieID`) 
    references Movie(`MovieID`) on delete no action;