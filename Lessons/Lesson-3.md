#  Mutations 

Mutations are queries that make changes or you could say mutate data. 

<!-- > -->

## Learning Objectives

1. Describe mutations
1. Define mutation queries 
1. Use Mutations 
1. Describe Resolvers

<!-- > -->

## Review

Schema's are a core feature of GraphQL. 

- Write a schema to describe a video game
	- title
	- studio
	- rating
	- genre
- Use an enum for the genre
- Write a type that represents a list of Video Games

<!-- > -->

## Resolvers 

Resolvers are where most of the magic happens in a GraphQL server. 

<!-- > -->

Each field in your schema is backed by a resolver function whose responsibility it is to return the data for that field. 

<!-- > -->

To turn that around, GraphQL queries are possible because there is a resolver function for each field. 

<!-- > -->

Imagine the type: 

```JS
type Time {
	hour: Int!
	minute: Int!
	second: Int!
}

type Query {
	getTime: Time!
}
```

<!-- > -->

To resolve Time we need a function that returns the values defined in it's fields: 

```JS
const root ={
	getTime: () => {
		const now = new Date()
		const hour = now.getHours()
		const minute = now.getMinutes()
		const second = now.getSeconds()
		return { hour, minute, second }
	}
}
```

<small>(Here we're resolving the getTime Query to a Time type)</small>

<!-- > -->

You might also define a resolver for each field. 

```JS
type Query {
	Time: Time!
}

const root = {
	Time: {
		hour: () => new Date().getHours(),
		minute: () => new Date().getMinutes(),
		second: () => new Date().getSeconds()
	}
}
```

<small>Here the Time type defines a resolver for each field.</small>

<!-- > -->

## Mutations

<!-- > -->

So far you've been using queries to get things from your GraphQL server. This is a like GET request with a REST server. 

Mutations are used to make changes at your GraphQL server. This is like a POST request with a REST server. 

<!-- > -->

Define a mutation with: 

```JS
type Mutation {
	...
}
```

<!-- > -->

Usually a Mutation will a function that takes some parameters: 

```JS
type Mutation {
	createUser(name: String!): User!
	post(url: String!, description: String!): Link!
}
```

<small>Mutations often return the thing they create, User, or Link in this example.</small>

<!-- > -->

When making a mutation query you'll start with the word "mutation"

```JS
mutation {
	createUser(name: "Jo") {
		name
		id
	}
}
```

<!-- > -->

Note! Queries start with the key word Query. But we've been omitting it. 

```JS
Query {
	getUsers {
		name
	}
}
```

<!-- > -->



<!-- > -->

## After Class 

- Start the GraphQL Node Tutorial: https://www.howtographql.com/graphql-js/0-introduction/

<!-- > -->

## Resources

- https://www.howtographql.com/graphql-js/0-introduction/
- 