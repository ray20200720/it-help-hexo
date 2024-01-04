title: yaml
date: 2024-01-04 13:44
categories: yaml, yml
------------------------

昨天上課時,聽到OpenAPI和yaml,發現自己不懂yaml/yml. 上網查了之後,在這邊做一下筆記

### 基本語法

`#` 是註解

`---` 三個破折號表示檔案開始
`...` 三個點表示檔案結束

檔案的結構是用 `key: value` 的方式

列表是以 `-` 或 ` ` 兩個空格

``` yaml
#Comment: Student record 
#Describes some characteristics and preferences
--- 
name: Martin D'vloper 
#key-value 
age: 26 
hobbies: 
  - painting 
  #first list item 
  - playing_music 
  #second list item 
  - cooking 
  #third list item 
programming_languages: 
  java: Intermediate 
  python: Advanced 
  javascript: Beginner 
favorite_food: 
  - vegetables: tomatoes 
  - fruits: 
      citrics: oranges 
      tropical: bananas 
      nuts: peanuts 
      sweets: raisins 
```

以上資料轉換成 JSON後如下

``` json
[
	{
		"name": "Martin D'vloper",
		"age": 26,
		"hobbies": [
			"painting",
			"playing_music",
			"cooking"
		],
		"programming_languages": {
			"java": "Intermediate",
			"python": "Advanced",
			"javascript": "Beginner"
		},
		"favorite_food": [
			{
				"vegetables": "tomatoes"
			},
			{
				"fruits": {
					"citrics": "oranges",
					"tropical": "bananas",
					"nuts": "peanuts",
					"sweets": "raisins"
				}
			}
		]
	}
]
```

### 參考資料

- [yaml beginners](https://www.redhat.com/sysadmin/yaml-beginners)
- [YAML 基本使用筆記](https://www.letswrite.tw/yaml-basic/)
- [What is yaml?](https://www.redhat.com/zh/topics/automation/what-is-yaml)
- [yaml introduction](https://www.w3schools.io/file/yaml-introduction/)
- [YAML 入门教程](https://www.runoob.com/w3cnote/yaml-intro.html)

### 工具

- https://jsonformatter.org/yaml-to-json

- https://www.json2yaml.com/convert-yaml-to-json

- https://onlineyamltools.com/convert-yaml-to-json