* https://sequelize.org/docs/v6/

## introduction



## getting started
* connecting to a db
* closing the connection
* logging



## core concepts

### model basics: https://sequelize.org/docs/v6/core-concepts/model-basics/
* define
* init: extending model
	* Foo.create({})
* table name
* model sync, all models at once
* dropping table, to drop all tables
* timestamp
* data type: https://sequelize.org/docs/v6/core-concepts/model-basics/#data-types
* column: https://sequelize.org/docs/v6/core-concepts/model-basics/#column-options

### model instances: https://sequelize.org/docs/v6/core-concepts/model-instances/
* create
	* foo = Foo.build({}); foo.save()
	* foo = await Foo.create()
* update
	* await foo.update({})
* delete
	* await foo.destroy()
* reload()
* increment({'foo', { by: 2 }})

### model querying - basics
* insert
	* await Foo.create(reqs, { fields: [] })
* select
	* await Foo.findAll()
	* Foo.findAll({ attributes: ['bar'] })
	* Foo.findAll({ attributes: { exclude: ['bar'] } })
* where: https://sequelize.org/docs/v6/core-concepts/model-querying-basics/#applying-where-clauses
	* Foo.findAll({ where: { bar: 1 } })
	* Foo.findAll({ where: { bar: [Op.gte]: 1 } })
* sequelize.fn(), sequelize.col()
* update query
	* await Foo.update({ bar: 'bar' }, { where: { bar: null } })
* delete query
	* await Info.destroy({ where: { id: ctx.params.id } })
* 


### model querying - finders

### getters, setters & virtuals

### validations & constraints

### raw queries

### associations

### paranoid



## advanced association concepts

### eager loading

### create with associations

### advanced M:N associations

### association scopes

### polymorphic associations



## other topics

### using sequelize in AWS lambda

### connection pool

### constrains & circularities

### dialect-specific things

### extending data types

### hooks

### indexes

### working with legacy tables

### legal notice

### migrations

### naming strategies

### optimistic locking

### other data types

### query interface

### read replication

### resources

### scopes

### sub queries

### transactions

### typescript

### upgrade to v6