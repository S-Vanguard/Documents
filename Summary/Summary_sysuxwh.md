# SWAPI项目总结
Author：16340256 谢玮鸿  

这次项目我和 熊秭鉴([@Xiongzj5](https://github.com/Xiongzj5)) 同学一起负责SWAPI的数据搜集、建立数据库，以及完成[git page](https://s-vanguard.github.io/)。经过协商，由我先开始编写一个网络爬虫程序，爬取 [The Star Wars API](https://swapi.co/) 网站上的数据。  

其实一开始我也没接触过爬虫，觉得爬虫大概是件比较困难的事情。不过多学有益，而且我对爬虫也比较感兴趣，因此我先开始从网上的博客学习，逐步地尝试模拟打开浏览器、打开特定的网站、获取html元素、文件输出等。  

该网络爬虫使用python语言编写，由于爬虫代码本身跟SWAPI项目没什么关系，于是在这次的项目中我commit次数最少... 不过代码上传到了我的个人仓库中：[sysuxwh/Web-Scrawler/SWAPI](https://github.com/sysuxwh/Web-Crawler/tree/master/SWAPI)。 接下来讲一讲爬虫是怎么实现的，以及与BoltDB的对接。  

---

## Selenium库的使用  
Selenium 是为了测试而出生的。但是没想到到了爬虫的年代, 它摇身一变, 变成了爬虫的好工具。用一句话简单来概括 Seleninm: **它能控制你的浏览器, 有模有样地学人类”看”网页**。  

使用Selenium库之前先要做以下准备：  
 * 安装Selenium库 ~~(废话)~~
   * 在终端中输入命令 `pip install selenium` 即可。
 * 下载浏览器的驱动  
   * Selenium库可以操控浏览器，通过浏览器驱动来启动浏览器。Selenium 针对几个主流的浏览器都有 driver（如Chrome, Firefox, Edge, Safari等）。我使用的是chrome浏览器，其安装的时候并不会附带driver，需要自行下载：[chrome driver](https://sites.google.com/a/chromium.org/chromedriver/downloads)
 * 将浏览器驱动添加到环境变量
   * 将驱动所在目录添加到环境变量后，会方便使用。其实不添加也行，只不过每次调用浏览器的时候都要指定驱动，比较麻烦。  
  
准备完毕后，就可以在python代码中使用了。如我们打开要爬取数据的网站：
``` python
from selenium import webdriver

browser = webdriver.Chrome()
base_url = "https://swapi.co/"
browser.get(base_url)
```
调用webdriver的`Chrome()`方法驱动浏览器开启，在使用`Chrome().get()`方法打开目标网站。  

selenium能做的事情很多很多，除了“看”网页，还能截图、模拟人类操作等等。但是这次我们只需要“看”和“记”的功能就行了，通过调用`find_element_by_xpath()`方法可以获取满足条件的html元素，非常方便。获取到想要的元素后，转换成特定的类型，然后输出到文件中，既可以完成爬虫工作。

---

## SWAPI的数据爬取  
这次项目爬取的数据有 61个星球，37艘飞船，39辆车辆，87个人，7部电影，37个种族。
``` python
    count = {'planets':61, 'starships':37, 'vehicles':39, 'people':87, 'films':7, 'species':37}

    for key in count:
        GetSearchContent(key, count[key])
```
为了简化数据的获取，与其选择在网页上输入数据名称（如输入'people/1/')，还不如直接调用该网站的API接口，以json格式显示 (如'https://swapi.co/api/starships/9/?format=json')。这样一来，可以省下 获取输入框元素、填充文本信息、点击搜索按钮、获取信息文本框等操作，方便不少。具体的爬取函数如下：  
``` python
def GetSearchContent(key, num):
    initXls(key)
    i = 0
    while i < num:
        browser.get(base_url + 'api/'+ key + '/' + str(count) + '/?format=json')
        text = browser.find_element_by_xpath("//pre").text
        print('Get data of ' + key + ' ' + str(count) + ' (' + str(i) + '/' + str(num) + ')')
        writeXls(key, count, text)  
        i = i + 1
```
但是在第一次成功爬取之后，发现爬取到了很多不存在的数据。原来该网站上面的数据并不是从1开始按顺序编号的，比如‘starships/1/’的数据就不存在，因此要更改一下代码。

``` python
def GetSearchContent(key, num):
    initXls(key)
    count = 0
    i = 0
    while i < num:
        count = count + 1
        browser.get(base_url + 'api/'+ key + '/' + str(count) + '/?format=json')
        text = browser.find_element_by_xpath("//pre").text
        if text != '{"detail":"Not found"}':
            i = i + 1
            print('Get data of ' + key + ' ' + str(count) + ' (' + str(i) + '/' + str(num) + ')')
            writeXls(key, count, text)  
```
这下爬取到的数据就是完整的、所需的数据了。  

---

## 数据的文件输出  
爬取到的数据要输出到哪里呢？经过商量，决定输出到excel文件中。一开始我选择调用了xlwt库，可以操作excel生成xls文件，使用简单方便。  

xlwt是一个纯粹的Excel Writer，因为它只能对Excel进行写操作。这次用到的操作有：
``` python
import xlwt
outfile = xlwt.Workbook(encoding = 'urf-8') # 新建一个Excel文件
sheet = outfile.add_sheet("XXX")            # 新建一个名为XXX的Sheet
sheet.write(row, col, data)                 # 在第row行第col列写入data
outfile.save("./StarWars.xls")              # 保存xls文件
```  
我输出的信息有三列：信息类型(people, starships等)，序号，json数据。  

到此，爬取数据的工作就做完了，然后去跟同学对接时发现还存在着点问题。

首先，golang没有读取xls文件的库，只能读取xlsx文件（前者是03版Office工作本格式，后者是07版及以后的Office工作本格式）。因此`.xls`没办法处理。本着认真至上的心，我决定不使用转换软件，而是从python文件修改。然而xlwt库不支持xlsx文件，只能调用更新的openpyxl库。

openpyxl支持最新版的Excel文件格式，对Excel文件具有响应的读写操作，对此有专门的Reader和Writer两个类，便于对Excel文件的操作。
``` python
from openpyxl.workbook import Workbook  
wbook = Workbook()                  # 新建一个Excel文件
sheet = wbook.create_sheet()        # 新建一个Sheet
sheet.title = key                   # 修改Sheet的名字
sheet['A%s'%(row)] = data           # 在A？列写入data
wbook.save("./StarWars.xlsx")       # 保存xlsx文件
```
与xlwt最大的不同就是获取坐标的方式，xlwt提供行数、列数即可，而openpyxl使用的是Excel里的索引方式。好在这次输出的列数不多，就直接用A B C代替0-2循环了，或者调用`openpyxl.cel`的`get_column_letter`方法将数字转换为字母列数表示也可。  

到这里还没结束，在学习BoltDB的过程中，了解到BoltDB数据库最大的特点是它采用键值对的方式来存储数据，为了让另一位同学更好地读入数据，我决定将第一列的信息类型去掉，输出设置成第一列是序号，第二列是json数据，这样更符合BoltDB的存储格式。

这下爬取数据的工作算是彻底完成了，接下来就是帮助完成数据库的构建，详情就看[另一个个人文档](https://github.com/Xiongzj5)啦。  

---

**最后一点关于git page想说的**  
其实好久没有接触过html了，写git page的时候老是在想html的各种元素标签是什么... 所以... 就多多支持我们的[git page](https://s-vanguard.github.io/)吧哈哈哈
