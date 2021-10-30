# 데이터베이스 

## Connect
```
cfg := os.Getenv("DBUSER")+":"+os.Getenv("DBPASS")+"@                 tcp(localhost:3306)/recordings"
db, err = sql.Open("mysql",cfg)
//os.Getenv("DBUSER")(환경변수 가져오기)
//cfg=db정보, sql.Open=첫번째인자:db종류,두번째인자:config
```
## Model
```
type Album struct {
    ID     int64
    Title  string
    Artist string
    Price  float32
}
```

## Find
```
db.Query("SELECT * FROM album WHERE artist = ?",name)
//첫번째 인자:쿼리문
//두번째인자 : 변수 
```

### Many Rows
```
for rows.Next() {                                                  
	var alb Album                                                  
	if err := rows.Scan(&alb.ID, &alb.Title, &alb.Artist, &alb.
    Price); 
	err != nil {
		return nil, fmt.Errorf("albumsByArtist %q: %v", name, err)         }                                                              
	albums = append(albums, alb)//배열에 alb 추가                                 
}
```

### Single row
```
var alb Album

    row := db.QueryRow("SELECT * FROM album WHERE id = ?", id)
    if err := row.Scan(&alb.ID, &alb.Title, &alb.Artist, &alb.Price); err != nil {
        if err == sql.ErrNoRows {
            return alb, fmt.Errorf("albumsById %d: no such album", id)
        }
        return alb, fmt.Errorf("albumsById %d: %v", id, err)
    }
    return alb, nil
	//sql.ErrNoRows:해당하는 열이 없다.
```

## Add data
```
result, err := db.Exec("INSERT INTO album (title, artist, price) VALUES (?, ?, ?)", alb.Title, alb.Artist, alb.Price)
    if err != nil {
        return 0, fmt.Errorf("addAlbum: %v", err)
    }
    id, err := result.LastInsertId()
    if err != nil {
        return 0, fmt.Errorf("addAlbum: %v", err)
    }
    return id, nil
	//db.Exec:쿼리문 실행
	//result.LastInsertId(): 제일 마지막으로 삽입된 열의 아이디
```
