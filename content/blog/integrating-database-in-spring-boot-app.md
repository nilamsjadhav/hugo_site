---
title: "Integrating Database in Spring Boot App"
date: 2023-03-19T21:56:45+05:30
draft: false
---

Before starting with integrating database in spring boot application let's understand some concept related to that.

* ORM :-  Object-relational mapping or ORM is the programming technique to map application domain model objects to the relational database tables. 

* Hibernate :- Hibernate is a Java-based ORM tool that provides a framework for mapping application domain objects to the relational database tables and vice versa.

* Database driver :- A database driver is a software that allows you to talk to your database from your application

* Connection pool :- A connection pool is a cache of database connections maintained so that the connections can be reused when future requests to the database are required.

## How to integrate database to spring boot application ?

let start with simple notes application having following endpoints :-
 - /notes/add-note -> To add note in application
 - /notes/get-notes -> To get all notes stored in application
 - /notes/remove-notes -> To remove all notes stored in application
    
  ```kotlin
    package com.example.DatabaseExp.controller

    import com.example.DatabaseExp.model.Note
    import com.example.DatabaseExp.service.NotesService
    import org.springframework.web.bind.annotation.*

    @RestController
    @RequestMapping("/notes")
    class NotesController(private val notesService: NotesService) {
      @GetMapping("/get-notes")
      fun getNotes(): MutableIterable<Note> {
        return notesService.get()
      }
      @PostMapping("/add-note")
      fun addNote(@RequestBody note: String):String{
        notesService.save(note)
        return "Note is add successfully"
      }
      @DeleteMapping("/remove-notes")
      fun removeNotes() {
        notesService.remove()
      }
    }
  ```

NotesService to call repository methods in order to perform various operations on database eg. save, find, remove, etc

```kotlin
  package com.example.DatabaseExp.service

  import com.example.DatabaseExp.model.Note
  import com.example.DatabaseExp.repository.NoteRepository
  import org.springframework.stereotype.Service
  import java.util.*

  @Service
  class NotesService(private val noteRepository: NoteRepository) {

    fun save(note: String) {
      noteRepository.save(Note(description = note, createdAt = Date()))
    }
    fun get(): MutableIterable<Note> {
      return noteRepository.findAll()
    }
    fun remove() {
      noteRepository.deleteAll()
    }
  }
```
Note model to create structure of table and store data in database 
```kotlin
  package com.example.DatabaseExp.model

  import java.util.*
  import javax.persistence.*

  @Entity
  @Table(name="notes")
  data class Note(
    @Id
    @Column
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    var id: Long? = null,

    @Column
    var description: String? = null,

    @Column
    var createdAt: Date? = null
  )
```
NoteRepository is extended from CrudRepository (can be extended from JPARepository) interface which have its abstract methods to do various operations on the database

```kotlin
  package com.example.DatabaseExp.repository

  import com.example.DatabaseExp.model.Note
  import org.springframework.data.repository.CrudRepository
  import org.springframework.stereotype.Repository

  @Repository
  interface NoteRepository : CrudRepository<Note, Int> {
    fun save(note: Note)
    fun findAllById(id:Int): Note
  }
```

#### Dependencies need to add into project to integrate database (eg. h2 database)
  * spring-boot-starter-data-jpa
  * com.h2database:h2

#### Some of the properties need to set for database integration 
  * spring.datasource.url
  
     This property specifies datasource path. It may be stored in file or memory. For instance, to store data in memory you can specify mem and after that storage name like this spring.datasource.url=jdbc:h2:mem:testdb.

  * spring.datasource.driver-class-name

    This property specifies driver name to connect with database. For example org.h2.Driver.

  * spring.jpa.database-platform

    This property is used to specify database name. Value could be org.hibernate.dialect.H2Dialect for h2 database.

  * spring.jpa.hibernate.ddl-auto

    This property specifies how Hibernate generates or updates the database schema.
    Values of this property are listed below :-
    1. create - Hibernate will drop the table and create it from scratch.
    2. create-drop - Hibernate will create a table when application is started and drop when it shutdown
    3. update - Hibernate updates the existing schema according to the entity mappings. It adds new tables, columns, or constraints but it does not drop the existing ones.
    4. validate - Hibernate validates the existing schema against the entity mappings. It does not make any changes to the database schema, but it reports any inconsistencies or errors.
    5. none - Hibernate does not perform any automatic schema generation or validation.