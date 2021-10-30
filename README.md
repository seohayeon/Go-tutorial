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

에러 생성 
errors.New("empty name")

nil (에러가 없다.)

로그 앞에 접두사(Ex: greetings:로그내용)
log.SetPrefix("greetings: ")

로그에 날짜/시간 없앤다.
log.SetFlags(0)

err출력후 프로그램 종료
log.Fatal(err)

배열 
```
[]string{"hello","hi","nice"}
```
배열에서 랜덤 인덱스 
```
rand.Intn(len(array))
```

## Modules
랜덤 숫자 math/rand package

콘솔 출력 fmt


## Others
모듈을 찾을 수 있는 곳 (npm과 비슷)
https://pkg.go.dev

function이름이 대문자로 시작하면 export가능

function이름이 소문자로 시작하면 export 불가능

출처
https://golang.org/doc/tutorial/
