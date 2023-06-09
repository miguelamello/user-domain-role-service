# User Domain Role Service

The User Domain Role Service provides a centralized and unified place to store and manage user roles across different domains or applications within a corporate environment. It can be used to implement a role-based access control system, where user access to various features, resources, or actions within each domain or application is determined by their assigned roles. This microservice can greatly simplify role management across corporate applications, ensure consistency in role assignments, and enhance security by implementing robust access controls.

## Architecture

- Go
- GraphQL
- MongoDB
- Redis
- Microservices
- GORM
- Gin

## Schema Design
In GraphQL schema design, we need to define the types and fields that will be exposed to the client applications. The schema also defines the queries and mutations that can be executed against the service. The following schema defines the types and operations supported by the User Domain Role Service:

```
  type User {
    id: ID!
    name: String!
    email: String!
    pwdhash: String!
    role: Role!
    domain: Domain!
    permissions: [Permission!]!
  }

  type Role {
    id: ID!
    name: String!
    description: String!
    permissions: [Permission!]!
  }

  type Domain {
    id: ID!
    name: String!
    description: String!
  }

  type Permission {
    id: ID!
    name: String!
    description: String!
  }

  type Query {
    userById(id: ID!): User
    userByName(name: String!): User
    userByEmail(email: String): User
    roles: [Role!]!
    domains: [Domain!]!
    permissions: [Permission!]!
  }

  input NewUser {
    name: String!
    email: String!
  }

  input UpdateUser {
    name: String!
    email: String!
    pwdhash: String!
    role: ID!
    domain: ID!
    permissions: [ID!]!
  }

  type Mutation {
    createUser(input: NewUser!): User!
    updateUser(id: ID!, input: UpdateUser!): User!
    deleteUser(id: ID!): User!
  }
```

[API Reference](https://github.com/miguelamello/user-domain-role-service/blob/main/reference.md)
## Implementation
### Centralized Role Management
The microservice acts as a central repository for storing and managing user roles. It can maintain a database or data store that associates users with their roles within different domains or applications.

### Role Mapping
The service allows administrators or authorized users to map roles to specific domains or applications. This mapping ensures that user roles are appropriately assigned and enforced within each application's context.

### Role-Based Access Control (RBAC)
The microservice can implement a role-based access control system, where user access to various features, resources, or actions within each domain or application is determined by their assigned roles. This ensures proper authorization and helps maintain data security.

### Role Synchronization
The "User Domain Role" service can provide mechanisms for synchronizing user roles across different applications or systems. When a role is updated or modified in the central service, it can trigger synchronization processes to propagate the changes to relevant applications, ensuring consistency and reducing manual efforts.

### Integration with Corporate Applications
The microservice should offer APIs or integration mechanisms that allow corporate applications to query and retrieve user roles based on the application's context. This enables seamless integration and eliminates the need for each application to maintain its own role management system.

### Role Assignment Workflow
The service can provide workflows for role assignment, ensuring that appropriate approval processes are followed. For example, when a user requests a new role, the system can route the request to the relevant approver(s) before the role is assigned.

### Audit and Logging
The microservice should incorporate logging and auditing capabilities to track role changes, access requests, and other relevant activities. This helps in compliance, troubleshooting, and maintaining an audit trail for security purposes.

### Scalability and Performance
The service should be designed to handle a large number of users and applications efficiently. Consider implementing caching mechanisms or optimized data structures to ensure fast and scalable retrieval of user roles.

### Security and Authentication
The microservice should enforce strong authentication and authorization mechanisms to protect the integrity and confidentiality of user roles. This may include implementing secure protocols, encryption, and access controls to safeguard sensitive data.

### User-Friendly Interface
Final step is building a user-friendly web interface or a dashboard that allows administrators to manage user roles, view role assignments, and monitor the overall health of the service.

By providing a centralized User Domain Role Service, we can simplify role management across corporate applications, ensure consistency in role assignments, and enhance security by implementing robust access controls. This microservice can greatly streamline user provisioning, access control, and compliance processes within the organization.

### Microservice Architecture

![Microservice Architecture](https://github.com/miguelamello/user-domain-role-service/blob/main/diagram.png)

Clients make requests to the GraphQL Api via HTTP POST protocol. The GraphQL service handle requests and process them by executing the corresponding queries and mutations. The service uses a Redis datastore to 
cache the results of the queries and mutations. Asyncronously the service updates the MongoDB with related data. The service uses a MongoDB database to store the data permanently. The service uses GORM (Go Object Relational Mapping) to interact with the MongoDB database. The service uses Gin framework to handle the HTTP requests. Everything is written and tied together if Go language, a very fast, typed and compiled language.



