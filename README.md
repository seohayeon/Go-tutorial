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
설치파일로 빌드한다. window(.exe) linux(./)
```
go build
```
설치 경로를 확인한다.
```
go list -f '{{.Target}}'
```
설치 경로를 바꾼다
```
go env -w GOBIN=/path/to/your/bin
```
설치 경로에 설치한다.
```
go install
```
테스트 파일을 실행한다
```
go test
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
map: map[key]value
```
make(map[string]string)

```
반복문 
```
for _, name := range names {
    //range의 names배열을 돌고 name은 그 배열의 요소  
	//예를 들어 names가  {"Gladys", "Samantha", "Darrin"} 라면 
	//반복문을 돌면서 배열에 있는 요소들을 뽑아온다.
    }
```
## Modules
랜덤 숫자 math/rand package

콘솔 출력 fmt


## Others
모듈을 찾을 수 있는 곳 (npm과 비슷)
https://pkg.go.dev

function이름이 대문자로 시작하면 export가능

function이름이 소문자로 시작하면 export 불가능

projectname_test.go라는 이름으로 테스트 파일을 만들 수 있다.

출처
https://golang.org/doc/tutorial/
