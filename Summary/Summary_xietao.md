
# 项目回顾

---

## 本人承担的工作
实现后端路由。主要是SWAPI那六个api，包括分页，衔接数据库和前端。

---

## 心得

### 1、mux的使用。

![](https://github.com/kataras/iris/raw/master/_benchmarks/benchmarks_third_party_source_snapshot_go_23_october_2018.png)

虽然感觉有点low，但是很骨感，算是比较接近没有框架的框架了，比较容易学到相对底层的很多东西，比如最基本的net/http包的使用。

基本使用模板可以是这样：

- 新建路由对象。这里其实封装了一层（为了提供后面说的路由日志功能），在sw.NewRouter的过程中，会调用mux.NewRouter。

```go
router := sw.NewRouter()
```

- 设置静态文件服务。这一步很重要，意思是开放public文件夹的Get权限，并引导以“/”开头的路由到public文件夹，比如要访问css便可以直接/css/xxx.css，要访问js则可以直接/js/xxx.js，若是不指定具体的文件，只输入/css或/js都会把对应/public/css和/pulic/js文件夹下的所有文件以一个链接的形式呈现在页面上。因此html中的引用逻辑和js中的跳转逻辑都可以直接写/css/xxx.css或/js/xxx.js或/html/xxx.html。

```go
router.PathPrefix("/").Handler(http.StripPrefix("/", http.FileServer(http.Dir("public"))))
```

- 监听端口并开始服务。这里直接使用的是http的ListenAndServe。

```go
http.ListenAndServe(":8080", router)
```

- 匹配和处理路由。这个是mux比较方便的地方，路由和路由处理都有统一的规范，比较适合处理批量路由和带变量的路由。
    - 首先定义一个结构体。Name是路由的名字，Method是请求的方法如Get、Post等，Pattern则是路由的url，HandlerFunc是路由的处理函数。

    ```go
    type Route struct {
        Name        string
        Method      string
        Pattern     string
        HandlerFunc http.HandlerFunc
    }
    ```

    - 然后定义一个路由数组。如下面的格式。

    ```go
    var routes = Routes{
	Route{
		"Index",
		"GET",
		"/",
		Index,
	},

	Route{
		"FilmsGet",
		strings.ToUpper("Get"),
		"/films",
		FilmsGet,
	},

	Route{
		"FilmsIdGet",
		strings.ToUpper("Get"),
		"/films/{id}",
		FilmsIdGet,
	},

    ...

    ```

    - 最后定义处理函数。以较简单的FilmsIdGet为例。

    ```go
    func FilmsIdGet(w http.ResponseWriter, r *http.Request) {
        w.Header().Set("Content-Type", "application/json; charset=UTF-8")
        id := strings.Trim(r.URL.Path, "/films/")
        json := db.GetFilmByID(id)
        if json == "" {
            w.WriteHeader(http.StatusNotFound)
            w.Write([]byte("404 Not found"))
        } else {
            w.WriteHeader(http.StatusOK)
            w.Write([]byte(json))
        }
    }
    ```

- 路由日志。这个便是sw的NewRouter的逻辑。其中Logger封装的一个用于输出格式化日志的函数。另外StrictSlash(true)表示认为/path和/path/是相同的，不作区分。

```go
func NewRouter() *mux.Router {
	router := mux.NewRouter().StrictSlash(true)
	for _, route := range routes {
		var handler http.Handler
		handler = route.HandlerFunc
		handler = Logger(handler, route.Name)

		router.
			Methods(route.Method).
			Path(route.Pattern).
			Name(route.Name).
			Handler(handler)
	}

	return router
}
```

### 2、 json的解析和构造。

- 这里需要用到官方支持的包

```go
import "encoding/json"
```

---

以下FilmsGet中处理分页的代码为例。

---

- 首先要有对应的结构体。定义形式如下，需要注明json。

```go
type FilmsList struct {

	// 记录数 
	Count int32 `json:"count,omitempty"`

	// 下一页（最后一页时该值为null） 
	Next string `json:"next,omitempty"`

	// 上一页（第一页时该值为null） 
	Previous string `json:"previous,omitempty"`

	Results []Films `json:"results,omitempty"`
}
```

```go
// the response type of films
type Films struct {

	// 记录被创建的时间
	Created time.Time `json:"created,omitempty"`

	// 记录被编辑的时间
	Edited time.Time `json:"edited,omitempty"`

	// 当前资源的URL
	Url string `json:"url,omitempty"`

	Title string `json:"title,omitempty"`

	EpisodeId int `json:"episode_id,omitempty"`

	OpeningCrawl string `json:"opening_crawl,omitempty"`

	Director string `json:"director,omitempty"`

	Producer string `json:"producer,omitempty"`

	ReleaseDate string `json:"release_date,omitempty"`

	Characters []string `json:"characters,omitempty"`

	Planets []string `json:"planets,omitempty"`

	Starships []string `json:"starships,omitempty"`

	Vehicles []string `json:"vehicles,omitempty"`

	Species []string `json:"species,omitempty"`
}
```

- 解析json。byte[] => json。核心函数是```json.Unmarshal(data []byte, v interface{}) error```。

```go
// set results
for i := 0; i < 10; i++ {
    if result[i] == "" {
        break
    }
    film := &Films{}
    err := json.Unmarshal([]byte(result[i]), &film)
    if err == nil {
        filmsList.Results = append(filmsList.Results, *film)
    } else {
        log.Fatal(err)
        return
    }
}
```

- 构造json。json => byte[]。核心函数是```json.Marshal(v interface{}) ([]byte, error)```。

```go
// make json of FilmsList
filmsList := &FilmsList{}
filmsList.Count = 7

// validation
...

// set next
...

// set previous
...

// set results
...

// make json to []byte, and response
b, err := json.Marshal(&filmsList)
if err == nil {
    w.WriteHeader(http.StatusOK)
    w.Write(b)
} else {
    log.Fatal(err)
}
```
