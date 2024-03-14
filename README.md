# vet.domains Subgraph

This Subgraph sources events from the vet.domains contracts. This includes the registry and any resolvers that are created and linked to domains. The resolvers are added through dynamic data sources. More information on all of this can be found at [The Graph Documentation](https://thegraph.com/docs/developer/quick-start/).

The original repository has been forked from: https://github.com/ensdomains/ens-subgraph

A deployment is available on: https://graph.vet/subgraphs/name/vns

# Example Queries

Here we have example queries, so that you don't have to type them in yourself eachtime in the graphiql playground:

```graphql
{
  domains {
    id
    labelName
    labelhash
    parent {
      id
    }
    subdomains {
      id
    }
    owner {
      id
    }
    resolver {
      id
    }
    ttl
  }
  resolvers {
    id
    address
    domain {
      id
    }
    events {
      id
      node
      ... on AddrChanged {
        a
      }
      ... on NameChanged {
        name
      }
      ... on AbiChanged {
        contentType
      }
      ... on PubkeyChanged {
        x
        y
      }
      ... on TextChanged {
        indexedKey
        key
      }
      ... on ContenthashChanged {
        hash
      }
      ... on InterfaceChanged {
        interfaceID
        implementer
      }
      ... on AuthorisationChanged {
        owner
        target
        isAuthorized
      }
    }
  }
  registrations(where: { labelName_not: null }, orderBy: expiryDate, orderDirection: asc, first: 10, skip: 0) {
    expiryDate
    labelName
    domain{
      name
      labelName
    }
  }
}

```