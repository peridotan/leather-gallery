---
---

<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>peridotan Leather Craft</title>

<style>
body{
  font-family:sans-serif;
  margin:0;
  background:#f5f5f5;
}

header{
  text-align:center;
  padding:30px;
  background:#222;
  color:white;
}

.gallery{
  max-width:1100px;
  margin:30px auto;
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(260px,1fr));
  gap:20px;
  padding:0 15px;
}

.card{
  background:white;
  border-radius:10px;
  overflow:hidden;
  box-shadow:0 2px 8px rgba(0,0,0,0.1);
}

.card img{
  width:100%;
  display:block;
}

.meta{
  padding:10px 12px;
}

.title{
  font-weight:bold;
}

.date{
  color:#666;
  font-size:12px;
}
</style>
</head>

<body>

<header>
<h1>peridotan Leather Craft</h1>
<p>images フォルダの画像を自動表示</p>
</header>

<div class="gallery">

{% assign files = site.static_files | sort: "name" | reverse %}

{% for file in files %}
{% if file.path contains '/images/' %}

{% assign name = file.name | remove: file.extname %}
{% assign parts = name | split: '_' %}
{% assign first = parts[0] %}
{% assign title = parts | shift | join: ' ' %}

{% if first contains '-' %}
{% assign date = first %}
{% else %}
{% assign title = name %}
{% assign date = '' %}
{% endif %}

<div class="card">

<img src="{{ file.path | relative_url }}">

<div class="meta">
<div class="title">{{ title | replace: '-', ' ' }}</div>
{% if date != '' %}
<div class="date">{{ date }}</div>
{% endif %}
</div>

</div>

{% endif %}
{% endfor %}

</div>

</body>
</html>