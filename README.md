# DeDeCMS
According to the individual needs a modified version

# Official
> 1. 官方网站  http://www.dedecms.com
> 2. 帮助手册	http://help.dedecms.com/index_old.htm

# Modify Source Code

> 修改栏目首字母

____


<p> 找到 /dede/catalog.add.php </p>

<pre>
	85: $toptypedir = GetPinyin(stripslashes($toptypename));
	$toptypedir = GetPinyin(stripslashes($toptypename),1);
	108: $typedir = $toptypedir.'/'.GetPinyin(stripslashes($v));
	$typedir = $toptypedir.'/'.GetPinyin(stripslashes($v),1);
	134: $toptypedir = GetPinyin(stripslashes($toptypename));
	$toptypedir = GetPinyin(stripslashes($toptypename),1);
	187: $typedir = GetPinyin(stripslashes($typename));
	$typedir = GetPinyin(stripslashes($typename),1); 
</pre>


> 修改发布文章时 keywords 字数限制

____

找到 /dede/article_add.php

<pre> sql: ALTER TABLE `dede_archives` MODIFY COLUMN `keywords`  char(255)
107：$keywords = cn_substrR($keywords,60);
$keywords = cn_substrR($keywords,255);
</pre>

> 采集完文章以后自动生成描述

____
找到 /dede/archives_do.php

<pre>
783： $allindexs = preg_replace("/#p#|#e#/",'',$sp->GetFinallyIndex());
后增加：
if($description=='' && $cfg_auot_description>0){
    $description = cn_substr(html2text($body),$cfg_auot_description);
    $description = trim(preg_replace('/#p#|#e#/','',$description));
    $description = addslashes($description);
}
</pre>

> 修改文章，不改变发布时间的方法

____

找到 /dede/templets/article_edit.htm
<pre>
464： $nowtime = GetDateTimeMk(time());
$nowtime = GetDateTimeMk($arcRow["pubdate"]);
</pre>


# Modify the function example
>1. 批量填加关键词 ( /dede/archives_do.php，/dede/js/list.js)

>2. 频道首页调用图集的第一张图片 ( /include/extend.func.php , /include/taglib/arclist.lib.php ) 调用方法： [field:first_imgurl/] 

>3. 列表页调用文章内容第一张图片(非缩略图)方法 （ /include/common.func.php ）调用方法：[field:litpic function='firstimg(@me)'/] 

>4. 自定义表单发邮件功能 （ /plus/diy.php.bak ）

>5. 添加批量增加tag标签功能 ( /dede/templates/content_list.htm ，/dede/js/list.js，/dede/archives_do.php )

####<p> 因为时间关系，还有很多修改功能没有展现出来，请有兴趣的自己研读代码吧！ </p>


