# Redis Adapter [![Godoc](https://pkg.go.dev/badge/github.com/mintxtinm/go-redis-adapter/v2)](https://pkg.go.dev/github.com/mintxtinm/go-redis-adapter/v2@v2.2.1)

Redis Adapter for go-redis is the [Redis](https://redis.io/) adapter for [Casbin](https://github.com/casbin/casbin), but with [go-redis] (https://github.com/go-redis/redis) as its client library. With this library, Casbin can load policy from Redis or save policy to it.

## Installation

    go get github.com/mintxtinm/go-redis-adapter/v2

## Simple Example

```go
package main

import (
	"github.com/casbin/casbin/v2"
	"github.com/mintxtinm/go-redis-adapter/v2"
)

func main() {
	// Initialize a Redis adapter and use it in a Casbin enforcer:
	a := redisadapter.NewAdapter("tcp", "127.0.0.1:6379") // Your Redis network and address.
	// Use the following if Redis has password like "123"
    //a := redisadapter.NewAdapterWithPassword("tcp", "127.0.0.1:6379", "123")
	e := casbin.NewEnforcer("examples/rbac_model.conf", a)

	// Load the policy from DB.
	e.LoadPolicy()

	// Check the permission.
	e.Enforce("alice", "data1", "read")

	// Modify the policy.
	// e.AddPolicy(...)
	// e.RemovePolicy(...)

	// Save the policy back to DB.
	e.SavePolicy()
}
```

## Getting Help

- [Casbin](https://github.com/casbin/casbin)

## License

This project is under Apache 2.0 License. See the [LICENSE](LICENSE) file for the full license text.
