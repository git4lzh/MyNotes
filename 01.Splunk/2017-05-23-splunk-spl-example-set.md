## Splunk一些SPL使用集合

|Example 1|
|----|
|index=main sourcetype=access\_combined \| table \_time referer\_domain, method, uri\_path, status, JSESSIONID, useragent|

|Example 2|
|----|
|index=main sourcetype=access\_combined \| table *|

|Example 3|
|----|
|index=main sourcetype=access\_combined \| fields - sourcetype, index, \_raw, source date* linecount punct host time* eventtype \| table *|

|Example 4|
|----|
|index=main sourcetype=access\_combined \| stats count by uri\_path \| sort - count|

|Example 5|
|----|
|index=main sourcetype=access\_combined \| top uri\_path|

|Example 6|
|----|
|index=main sourcetype=access\_combined \| top uri\_path limit=20|

|Example 7|
|----|
|index=main sourcetype=access\_combined \| stats dc(uri\_path) by user \| sort - user|

|Example 8|
|----|
|index=main sourcetype=access\_combined \| eval browser=useragent \| replace \*Firefox\* with Firefox, \*Chrome\* with Chrome, \*MSIE\* with "Internet Explorer", \*Version\*Safari\* with Safari, \*Opera\* with Opera in browser \| top limit=5 useother=t browser|

|Example 9|
|----|
|index=main sourcetype=access\_combined \| eval os=useragent \| replace \*Windows\* with Windows, \*Macintosh\* with Apple, \*Linux\* with Linux in os \| top limit=5 useother=t os|

|Example 10|
|----|
|index=main sourcetype=access\_combined \| stats dc(clientip) AS Referals by referer\_domain \| sort - Referals|

|Example 11|
|----|
|index=main sourcetype=access\_combined \| stats dc(clientip) AS Referals by referer\_domain \| sort - Referals \| head 10|

|Example 12|
|----|
|index=main sourcetype=access\_combined \| chart count(eval(like(status, "2%"))) AS Success, count(eval(like(status, "4%") OR like(status, "5%"))) AS Error by uri\_path|

|Example 13|
|----|
|index=main sourcetype=access\_combined uri\_path="/addItem" OR uri\_path="/checkout" \| chart count(eval(like(status, "2%"))) AS Success, count(eval(like(status, "4%") OR like(status, "5%"))) AS Error by uri\_path \| addcoltotals label=Total labelfield=uri\_path|

