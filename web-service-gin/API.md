# Go Api
Go에서 REST API를 만들어보자.

## SETTING
데이터 모델을 만든다.

`json:"key"`는 출력시 키이름
```
type album struct {
    ID     string  `json:"id"`
    Title  string  `json:"title"`
    Artist string  `json:"artist"`
    Price  float64 `json:"price"`
}
```

모델을 바탕으로 fake data를 만든다.
```
var albums = []album{
    {ID: "1", Title: "Blue Train", Artist: "John Coltrane", Price: 56.99},
    {ID: "2", Title: "Jeru", Artist: "Gerry Mulligan", Price: 17.99},
    {ID: "3", Title: "Sarah Vaughan and Clifford Brown", Artist: "Sarah Vaughan", Price: 39.99},
}
```

## GET
GET요청을 받으면 실행될 함수를 만든다.

아래코드는 GET요청시 albums의 값을 보낸다.

```
func getAlbums(c *gin.Context) {
    c.IndentedJSON(http.StatusOK//200, albums)
}
```

main()함수에 라우터를 등록하자.

서버가 8080포트에서 돌아가고 /albums라우터로 접근시 getAlbums함수를 실행한다.
```
func main() {
    router := gin.Default()
    router.GET("/albums", getAlbums)

    router.Run("localhost:8080")
}
```



## POST
post로 접속했을때 실행될 함수를 만든다.

c.BindJSON:요청의 body를 newAlbum에 바인딩한다.

append(albums,newAlbum): albums배열에 newAlbum을 추가한다.

```
func postAlbums(c *gin.Context) {
    var newAlbum album

    // Call BindJSON to bind the received JSON to
    // newAlbum.
    if err := c.BindJSON(&newAlbum); err != nil {
        return
    }

    // Add the new album to the slice.
    albums = append(albums, newAlbum)
    c.IndentedJSON(http.StatusCreated, newAlbum)
}
```

## GET PATH
path의 아이디와 아이디가 일치하는 데이터를 가져온다.

id := c.Param("id"):id 변수에 id param을 대입한다.

for문:albums를 돌면서 아이디가 param의 아이디와 일치하는것을 찾고 일치하면 200코드와 함께 일치하는 데이터를 보낸다.

만약 일치하는게 없으면 NotFound코드와 함께 album not found라는 결과를 보낸다.

```
func getAlbumByID(c *gin.Context) {
    id := c.Param("id")

    // Loop over the list of albums, looking for
    // an album whose ID value matches the parameter.
    for _, a := range albums {
        if a.ID == id {
            c.IndentedJSON(http.StatusOK, a)
            return
        }
    }
    c.IndentedJSON(http.StatusNotFound, gin.H{"message": "album not found"})
}
```

main()함수에 라우터를 등록한다.

router.GET("/albums/:id", getAlbumByID)
