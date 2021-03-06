# Using truss

## File structure

You start with your definition file, named `svc.proto`, in the current
directory. The current directory should look like this:

```
.
└── svc.proto
```

Then, you'd run truss on your service definition file, like this: `truss
svc.proto`.  After running truss on your service, `NAME-service` should be
created in your current directory. `NAME-service`, where NAME is the name of
the package defined in your definition file. Here's what that structure would
look like:

```
.
├── NAME-service
│   ├── docs
│   │   └── docs.md
│   ├── generated
│   │   └── ...
│   ├── handlers
│   │   └── server
│   │       └── server_handler.go
│   ├── NAME-cli-client
│   │   └── client_main.go
│   ├── NAME-server
│   │   └── server_main.go
│   ├── svc.pb.go
│   └── third_party
│       └── ...
├── svc.proto
```

Now that you've generated your service, you can install the generated binaries
with `go install ./...` which will install `NAME-cli-client` and `NAME-server`,
where NAME is the name of the package defined in your definition file.

To add business logic from this point, you'd edit the `server_handler.go` file
in `./NAME-service/handlers/server/`, where NAME is the name of the package
defined in your definition file.

## *Our Contact*

1. Only the files in `handlers/` are user modifiable. The only functions allowed in the handler files are exported functions with the same names as those defined as rpc's in the definition service; all other exported functions will be removed. User logic can be imported and executed within the functions in the handlers.
2. Do not create files or directories in `NAME-service/`
3. All user logic should exist outside of `NAME-service/`, leaving organization of that logic up to the user.
