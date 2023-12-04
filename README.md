# prometheuslog

all the configurations for this lib need to put into `config.yaml` file with the path set to environment `CONFIG_FILE`
```bash
export CONFIG_FILE=${CURDIR}/example/config/config.yaml
go run main.go
```

## flogging

Clone from flogging of Hyperledger Fabric:
https://github.com/hyperledger/fabric/tree/master/common/flogging

[1] `import flogging "github.com/Hnampk/prometheuslog/flogging"`

[2] Just define `logger = flogging.MustGetLogger("services.abc.xyz")`

[3] Then call `logger.Info(...)`, `logger.Warn(...)`, `logger.Error(...)` for logging

- sample configuration in `config.yaml` file:

```yaml
Log:
    Level: INFO # DEBUG/INFO/WARN/ERROR (default: DEBUG)
    Format: "%{color}%{time:2006-01-02 15:04:05.000 MST} [%{module}] %{shortfunc} -> %{level:.4s} %{id:03x}%{color:reset} %{message}" # default: json
```

## gotracing

trace the process duration of a function

```golang
import flogging "github.com/Hnampk/prometheuslog/gotracing"

var tracer = gotracing.MustGetTracer("mypackage")

func test(requestID string){
    tracer.StartFunction(requestID)
	defer accountTracer.EndFunctionWithDurationSince(requestID, time.Now())

    // do something
}
```

