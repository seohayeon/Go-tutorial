## Command
새로운 모듈을 생성합니다.
```
go mod init [module]
```

모듈을 추가합니다.
```
go mod tidy
```

example.com/greetings이라는 모듈을 import했는데 그 모듈이 상위폴더에 있을 때 모듈 위치를 지정함
```
go mod edit -replace example.com/greetings=../greetings
```
## File
콘솔출력
```
fmt.println()
```

%v가 name으로 대체된다. 
```
fmt.Sprintf("Hi, %v. Welcome!", name)
```

:= (var을 생략한다.)

## Others
모듈을 찾을 수 있는 곳 (npm과 비슷)
https://pkg.go.dev

출처
https://golang.org/doc/tutorial/
