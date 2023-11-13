

```go
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
```


проаналізуй все
```go
golangci-lint run -c "/home/evoplay/.gin/golangci-lint-config/.golangci.yml"
```

проаналізуй тільки змінені файли в гілці
```go
golangci-lint run -c "/home/evoplay/.gin/golangci-lint-config/.golangci.yml" --new-from-rev origin/master
```