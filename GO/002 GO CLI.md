---
tags:
 GO
 cli_commands
---

- [[go golangci-lint]]

### show dependencies which have newer versions available (аналог `composer outdated`)


```bash
go list -u -m all
```

### update all dependencies(only on minor/patch)

```bash
go get -u ./...
```

### update all dependencies(only on major/minor/patch)

```bash
go get -u=patch ./...
```