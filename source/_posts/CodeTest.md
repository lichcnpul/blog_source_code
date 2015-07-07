title: CodeTest
date: 2015-06-20 19:08:56
categories: Javascript
tags: thesis
toc: true
---
参考文献：[Hexo在github上构建免费的Web应用](http://blog.fens.me/hexo-blog-github/)
## Javascript
```javascript
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');

var Cat = mongoose.model('Cat',{
	name: String,
	friends: [String],
	age: Number,
});

var kitty = new Cat({name: 'Zildjian', friends: ['tom','jerry']});
kitty.age = 3;

kitty.save(function(err) {
	if(err) ;
	console.log('meow');
});
```
## Java
``` java
import javax.jws.WebMethod;
import javax.jws.WebService;
/*
 * SEI;
 */
@WebService
public interface HelloWS {

	@WebMethod
	public String sayHello(String name);
}
```
## Ruby
```ruby
@numtocodetable = Hash.[](
  "21" => "q",  "22" => "w",  "23" => "e",  "31" => "r",  "32" => "t",  "33" => "y",
  "41" => "u",  "42" => "i",  "43" => "o",  "51" => "p",  "52" => "a",  "53" => "s",
  "61" => "d",  "62" => "f",  "63" => "g",  "71" => "h",  "72" => "j",  "73" => "k",
  "74" => "l",  "81" => "z",  "82" => "x",  "83" => "c",  "91" => "v",  "92" => "b",
  "93" => "n",  "94" => "m"
)

  @codetonumtable = Hash.[](
  "q" => "21", "w" => "22", "e" => "23", "r" => "31", "t" => "32", "y" => "33",
  "u" => "41", "i" => "42", "o" => "43", "p" => "51", "a" => "52", "s" => "53",
  "d" => "61", "f" => "62", "g" => "63", "h" => "71", "j" => "72", "k" => "73",
  "l" => "74", "z" => "81", "x" => "82", "c" => "83", "v" => "91", "b" => "92",
  "n" => "93", "m" => "94"
)

def self.codetonum(code)
    num = ""
    codeinput = code
    codeinput.split(//).each do |item|
      num = num + @codetonumtable[item]
    end
    return num
end

def self.numtocode(num)
    p = ""
    input = num
    str = input.scan(/[0-9]{2}/)
    str.each do |item|
      p = p + @numtocodetable[item]
    end
    return p
end
```
## Python
```python
print('hello world')
```

## CSharp
``` csharp
using System;

namespace HelloWorld
{
	class MainClass
	{
		public static void Main (string[] args)
		{
			Console.WriteLine ("Hello World!");
		}
	}
}
```
