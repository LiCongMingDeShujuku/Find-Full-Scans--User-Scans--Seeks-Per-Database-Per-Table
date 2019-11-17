![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 搜索每个数据库每个表格，查找完整扫描（Full Scans）,用户扫描（User Scans）
#### Find Full Scans, User Scans, Seeks Per Database Per Table
**发布-日期: 2014年05月06日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这是一个快速脚本，向你显示在每个数据库，每个表格中进行用户扫描（User Scans），用户搜索（User Seeks）等。

## English
Here’s a quick script to show you the User Scans, User Seeks, etc per Database, Per table.

---
## Logic
```SQL

use MyDatabaseName;
set nocount on
select
	distinct
	--'database' = db_name(sddius.database_id),
	'table' = so.name
, 	'index' = si.name
, 	sddius.user_seeks
,	sddius.user_scans
, 	'last_user_seek' = convert(char, sddius.last_user_seek, 9)
, 	'last_user_scan' = convert(char, sddius.last_user_scan, 9)
from
sys.objects so join sys.indexes si on si.object_id = so.object_id
left outer join sys.dm_db_index_usage_stats sddius on si.index_id = sddius.index_id
where
db_name(sddius.database_id) is not null
and sddius.database_id &gt; 4
and user_scans &gt; 5
and so.type = 'u' and si.type_desc &lt;&gt; 'heap'
and last_user_scan &gt; (select getdate() - 5)

```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

