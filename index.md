<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>peridotan Leather Craft</title>

<style>
body{
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Hiragino Sans","Yu Gothic",sans-serif;
  margin:0;
  background:#f5f5f5;
  color:#222;
}

header{
  text-align:center;
  padding:30px 16px;
  background:#222;
  color:#fff;
}

.gallery{
  max-width:1100px;
  margin:30px auto;
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(260px,1fr));
  gap:20px;
  padding:0 15px 30px;
}

.card{
  background:#fff;
  border-radius:12px;
  overflow:hidden;
  box-shadow:0 2px 10px rgba(0,0,0,.08);
}

.card img{
  width:100%;
  aspect-ratio:4 / 5;
  object-fit:cover;
  display:block;
  background:#ddd;
}

.meta{
  padding:12px 14px 14px;
}

.title{
  font-size:16px;
  font-weight:700;
  line-height:1.4;
  word-break:break-word;
}

.date{
  margin-top:6px;
  color:#666;
  font-size:13px;
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
    {% assign ext = file.extname | downcase %}
    {% if ext == '.jpg' or ext == '.jpeg' or ext == '.png' or ext == '.webp' or ext == '.gif' %}
      {% assign basename = file.name | remove: file.extname %}
      {% assign display_date = '' %}
      {% assign display_title = basename %}

      {% if basename contains '_' %}
        {% assign first10 = basename | slice: 0, 10 %}
        {% assign char5 = basename | slice: 4, 1 %}
        {% assign char8 = basename | slice: 7, 1 %}

        {% if char5 == '-' and char8 == '-' %}
          {% assign display_date = first10 %}
          {% assign display_title = basename | remove_first: first10 | remove_first: '_' %}
        {% endif %}
      {% endif %}

      <div class="card">
        <img src="{{ file.path | relative_url }}" alt="{{ display_title | replace: '_', ' ' | replace: '-', ' ' }}">
        <div class="meta">
          <div class="title">{{ display_title | replace: '_', ' ' | replace: '-', ' ' }}</div>
          {% if display_date != '' %}
            <div class="date">{{ display_date }}</div>
          {% endif %}
        </div>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}
</div>

</body>
</html>