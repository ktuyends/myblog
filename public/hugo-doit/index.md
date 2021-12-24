# Khám Phá Theme Hugo DoIt


<!--more-->

## 1. Tạo blog trong vài phút

**Chuẩn bị:**

- R và RStudio, sau đó cài đặt package Blogdown

Bước 1: Tạo blog ở local

- File -> New Project -> Blogdown -> New Directory -> Website using Blogdown

![](./images/blogdown.png)

Xem Website ở local

```bash
hugo serve --disableFastRender
```

Sau đó vào trang: `http://localhost:1313`

Bước 2: Push blog lên GitHub

- Tạo repository, sau đó:

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git add remote <url>
git push origin main
```

Bước 3: Build blog bằng [netlify](https://www.netlify.com/)

- Đăng nhập Netlify bằng GitHub
- Chọn `New site from Git > Continuous Deployment: GitHub`
- Chọn Repository của Blog, sau đó chọn Deploy site
- Chọn Domain Setting để chỉnh sửa lại tên miền

## 2. Tùy chỉnh Blog

Một số lưu ý trước khi chỉnh sửa:

Ảnh và file chứa trong `assets` và `static`

Truy cập thông qua link: `/assets/...` và `/static/...`

CDN được lưu trữ ở `/assets/data/cdn/...`

Favicon: `/static/...`

Color: `browserconfig.xml` và `browserconfig.xml`

Style: `assets/css/_override.scss` và `assets/css/_custom.scss`

Font:

Comment: 

Menu

```scss
@import url('https://fonts.googleapis.com/css?family=Fira+Mono:400,700&display=swap&subset=latin-ext');
$code-font-family: Fira Mono, Source Code Pro, Menlo, Consolas, Monaco, monospace;
```

## 2.1. Chỉnh sửa file config.toml

```toml
baseURL = "https://ktuyends.netlify.app"

# [en, vi, fr, pl, ...] determines default content language
defaultContentLanguage = "en"

# theme
theme = "DoIt"

# website title
title = "Tuyen's Blog"

# whether to use robots.txt
enableRobotsTXT = true

# whether to use git commit log
enableGitInfo = true

# whether to use emoji code
enableEmoji = true

[languages]
  [languages.vi]
    weight = 1
    # language code
    languageCode = "vi"
    # language name
    languageName = "Vietnamese"
    # whether to include Chinese/Japanese/Korean
    hasCJKLanguage = false
    # default amount of posts in each pages
    paginate = 12
    # [UA-XXXXXXXX-X] google analytics code
    googleAnalytics = ""
    # copyright description used only for seo schema
    copyright = "This work is licensed under a Creative Commons Attribution-NonCommercial 4.0 International License."
    # Menu config
    [languages.vi.menu]
      [[languages.vi.menu.main]]
        identifier = "posts"
        # you can add extra information before the name (HTML format is supported), such as icons
        pre = ""
        # you can add extra information after the name (HTML format is supported), such as icons
        post = ""
        name = "Posts"
        url = "/posts/"
        # title will be shown when you hover on this menu link.
        title = ""
        weight = 1
      [[languages.vi.menu.main]]
        identifier = "tags"
        pre = ""
        post = ""
        name = "Tags"
        url = "/tags/"
        title = ""
        weight = 2
      [[languages.vi.menu.main]]
        identifier = "categories"
        pre = ""
        post = ""
        name = "Categories"
        url = "/categories/"
        title = ""
        weight = 3
      [[languages.vi.menu.main]]
        identifier = "series"
        pre = ""
        post = ""
        name = "Series"
        url = "/series/"
        title = ""
        weight = 4
      [[languages.vi.menu.main]]
        identifier = "authors"
        pre = ""
        post = ""
        name = "Authors"
        url = "/authors/"
        title = ""
        weight = 5
      [[languages.vi.menu.main]]
        identifier = "showcase"
        pre = ""
        post = ""
        name = "Showcase"
        url = "/showcase/"
        title = ""
        weight = 6
      [[languages.vi.menu.main]]
        identifier = "documentation"
        pre = ""
        post = ""
        name = "Docs"
        url = "/categories/documentation/"
        title = ""
        weight = 7
      [[languages.vi.menu.main]]
        identifier = "about"
        pre = ""
        post = ""
        name = "About"
        url = "/about/"
        title = ""
        weight = 8
      [[languages.vi.menu.main]]
        identifier = "github"
        pre = "<i class='fab fa-github fa-fw'></i>"
        post = ""
        name = ""
        url = "https://github.com/ktuyends"
        title = "GitHub"
        weight = 9
    [languages.vi.params]
      # site description
      description = "Sometimes I write something just so that I can go back and read it"
      # site keywords
      keywords = ["little Things", "Data", "Data Science", "Business Intelligence", "Business Analytics"]
      # App icon config
      [languages.vi.params.app]
        # optional site title override for the app when added to an iOS home screen or Android launcher
        title = "Tuyen Kieu"
        # whether to omit favicon resource links
        noFavicon = false
        # modern SVG favicon to use in place of older style .png and .ico files
        svgFavicon = ""
        # Safari mask icon color
        iconColor = "#5bbad5"
        # Windows v8-10 tile color
        tileColor = "#da532c"
      # Search config
      [languages.vi.params.search]
        enable = true
        # type of search engine ("lunr", "algolia", "fuse")
        type = "lunr"
        # max index length of the chunked content
        contentLength = 4000
        # placeholder of the search bar
        placeholder = ""
        # max number of results length
        maxResultLength = 10
        # snippet length of the result
        snippetLength = 300
        # HTML tag name of the highlight part in results
        highlightTag = "em"
        # whether to use the absolute URL based on the baseURL in search index
        absoluteURL = false
        [languages.vi.params.search.algolia]
          index = "en_index"
          appID = "5YGRNRQK1G"
          searchKey = "0ff6874805de24b84aa1d5ebccad56cd"
        [languages.vi.params.search.fuse]
          # https://fusejs.io/api/options.html
          isCaseSensitive = false
          minMatchCharLength = 2
          findAllMatches = false
          location = 0
          threshold = 0.1
          distance = 100
          ignoreLocation = true
          useExtendedSearch = false
          ignoreFieldNorm = false
      # Home page config
      [languages.vi.params.home]
        # amount of RSS pages
        rss = 10
        # Home page profile
        [languages.vi.params.home.profile]
          enable = true
          # Gravatar Email for preferred avatar in home page
          gravatarEmail = "ktuyen.ds@gmail.com"
          # URL of avatar shown in home page
          avatarURL = ""
          # title shown in home page (HTML format is supported)
          title = ""
          # subtitle shown in home page
          subtitle = "Sometimes I write something just so that I can go back and read it"
          # whether to use typeit animation for subtitle
          typeit = true
          # whether to show social links
          social = true
          # disclaimer (HTML format is supported)
          disclaimer = ""
        # Home page posts
        [languages.vi.params.home.posts]
          enable = true
          # special amount of posts in each home posts page
          paginate = 7
      # Social config in home page
      [languages.vi.params.social]
        GitHub = "ktuyends"
        Linkedin = "ktuyends"
        Email = "ktuyen.ds@gmail.com"
        Facebook = "ktuyends"
        Skype = "live:.cid.5deb017f815a755d"
      # Sponsor config
      [languages.vi.params.sponsor]
        enable = false
        bio = "If you find this post helpful, please consider sponsoring."
        link = "https://github.com/sponsors/ktuyends"
        # custom = "<a href=\"https://www.buymeacoffee.com/ktuyends\" target=\"_blank\"><img src=\"https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png\" alt=\"Buy Me A Coffee\" style=\"height: 40px !important;width: 145 !important;\" ></a>"

  [languages.en]
    weight = 2
    # language code
    languageCode = "en"
    # language name
    languageName = "English"
    # whether to include Chinese/Japanese/Korean
    hasCJKLanguage = false
    # default amount of posts in each pages
    paginate = 12
    # [UA-XXXXXXXX-X] google analytics code
    googleAnalytics = ""
    # copyright description used only for seo schema
    copyright = "This work is licensed under a Creative Commons Attribution-NonCommercial 4.0 International License."
    # Menu config
    [languages.en.menu]
      [[languages.en.menu.main]]
        identifier = "posts"
        # you can add extra information before the name (HTML format is supported), such as icons
        pre = ""
        # you can add extra information after the name (HTML format is supported), such as icons
        post = ""
        name = "Posts"
        url = "/posts/"
        # title will be shown when you hover on this menu link.
        title = ""
        weight = 1
      [[languages.en.menu.main]]
        identifier = "tags"
        pre = ""
        post = ""
        name = "Tags"
        url = "/tags/"
        title = ""
        weight = 2
      [[languages.en.menu.main]]
        identifier = "categories"
        pre = ""
        post = ""
        name = "Categories"
        url = "/categories/"
        title = ""
        weight = 3
      [[languages.en.menu.main]]
        identifier = "series"
        pre = ""
        post = ""
        name = "Series"
        url = "/series/"
        title = ""
        weight = 4
      [[languages.en.menu.main]]
        identifier = "authors"
        pre = ""
        post = ""
        name = "Authors"
        url = "/authors/"
        title = ""
        weight = 5
      [[languages.en.menu.main]]
        identifier = "showcase"
        pre = ""
        post = ""
        name = "Showcase"
        url = "/showcase/"
        title = ""
        weight = 6
      [[languages.en.menu.main]]
        identifier = "documentation"
        pre = ""
        post = ""
        name = "Docs"
        url = "/categories/documentation/"
        title = ""
        weight = 7
      [[languages.en.menu.main]]
        identifier = "about"
        pre = ""
        post = ""
        name = "About"
        url = "/about/"
        title = ""
        weight = 8
      [[languages.en.menu.main]]
        identifier = "github"
        pre = "<i class='fab fa-github fa-fw'></i>"
        post = ""
        name = ""
        url = "https://github.com/ktuyends"
        title = "GitHub"
        weight = 9
    [languages.en.params]
      # site description
      description = "Sometimes I write something just so that I can go back and read it"
      # site keywords
      keywords = ["little Things", "Data", "Data Science", "Business Intelligence", "Business Analytics"]
      # App icon config
      [languages.en.params.app]
        # optional site title override for the app when added to an iOS home screen or Android launcher
        title = "Tuyen Kieu"
        # whether to omit favicon resource links
        noFavicon = false
        # modern SVG favicon to use in place of older style .png and .ico files
        svgFavicon = ""
        # Safari mask icon color
        iconColor = "#5bbad5"
        # Windows v8-10 tile color
        tileColor = "#da532c"
      # Search config
      [languages.en.params.search]
        enable = true
        # type of search engine ("lunr", "algolia", "fuse")
        type = "lunr"
        # max index length of the chunked content
        contentLength = 4000
        # placeholder of the search bar
        placeholder = ""
        # max number of results length
        maxResultLength = 10
        # snippet length of the result
        snippetLength = 300
        # HTML tag name of the highlight part in results
        highlightTag = "em"
        # whether to use the absolute URL based on the baseURL in search index
        absoluteURL = false
        [languages.en.params.search.algolia]
          index = "en_index"
          appID = "5YGRNRQK1G"
          searchKey = "0ff6874805de24b84aa1d5ebccad56cd"
        [languages.en.params.search.fuse]
          # https://fusejs.io/api/options.html
          isCaseSensitive = false
          minMatchCharLength = 2
          findAllMatches = false
          location = 0
          threshold = 0.1
          distance = 100
          ignoreLocation = true
          useExtendedSearch = false
          ignoreFieldNorm = false
      # Home page config
      [languages.en.params.home]
        # amount of RSS pages
        rss = 10
        # Home page profile
        [languages.en.params.home.profile]
          enable = true
          # Gravatar Email for preferred avatar in home page
          gravatarEmail = "ktuyen.ds@gmail.com"
          # URL of avatar shown in home page
          avatarURL = ""
          # title shown in home page (HTML format is supported)
          title = ""
          # subtitle shown in home page
          subtitle = "Sometimes I write something just so that I can go back and read it"
          # whether to use typeit animation for subtitle
          typeit = true
          # whether to show social links
          social = true
          # disclaimer (HTML format is supported)
          disclaimer = ""
        # Home page posts
        [languages.en.params.home.posts]
          enable = true
          # special amount of posts in each home posts page
          paginate = 7
      # Social config in home page
      [languages.en.params.social]
        GitHub = "ktuyends"
        Linkedin = "ktuyends"
        Email = "ktuyen.ds@gmail.com"
        Facebook = "ktuyends"
        Skype = "live:.cid.5deb017f815a755d"
      # Sponsor config
      [languages.en.params.sponsor]
        enable = false
        bio = "If you find this post helpful, please consider sponsoring."
        link = "https://github.com/sponsors/ktuyends"
        # custom = "<a href=\"https://www.buymeacoffee.com/ktuyends\" target=\"_blank\"><img src=\"https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png\" alt=\"Buy Me A Coffee\" style=\"height: 40px !important;width: 145 !important;\" ></a>"

[params]
  # website title
  title = "Tuyen's Blog"
  # DoIt theme version
  version = "0.2.X"
  # site default theme ("light", "dark", "black", "auto")
  defaultTheme = "dark"
  # public git repo url only then enableGitInfo is true
  gitRepo = ""
  # which hash function used for SRI, when empty, no SRI is used ("sha256", "sha384", "sha512", "md5")
  fingerprint = ""
  # date format
  dateFormat = "2006-01-02"
  # website images for Open Graph and Twitter Cards
  images = ["/images/avatar.webp"]
  # enable PWA
  enablePWA = true  
  # license information
  license = '<a rel="license external nofollow noopener noreffer" href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank">CC BY-NC 4.0</a>'

  # Header config
  [params.header]
    # desktop header mode ("fixed", "normal", "auto")
    desktopMode = "fixed"
    # mobile header mode ("fixed", "normal", "auto")
    mobileMode = "auto"
    # theme change mode ("switch", "select")
    themeChangeMode = "select"
    # Header title config
    [params.header.title]
      # URL of the LOGO
      logo = ""
      # title name
      name = "Tuyen's Blog"
      # you can add extra information before the name (HTML format is supported), such as icons
      pre = ""
      # you can add extra information after the name (HTML format is supported), such as icons
      post = ""
      # whether to use typeit animation for title name
      typeit = false

  # Footer config
  [params.footer]
    enable = true
    # Custom content (HTML format is supported)
    custom = ''
    # whether to show Hugo and theme info
    hugo = false
    # whether to show copyright info
    copyright = true
    # whether to show the author
    author = true
    # site creation time
    since = 2019
    # ICP info only in China (HTML format is supported)
    icp = ""
    # license info (HTML format is supported)
    license= 'Powered by <a href="https://gohugo.io/">Hugo</a> & <a href="https://github.com/HEIGE-PCloud/DoIt">DoIt</a>'

  # Section (all posts) page config
  [params.section]
    # special amount of posts in each section page
    paginate = 12
    # date format (month and day)
    dateFormat = "01-02"
    # amount of RSS pages
    rss = 10
    # recently updated posts settings
    [params.section.recentlyUpdated]
      enable = true
      rss = true
      days = 30
      maxCount = 3

  # List (category or tag) page config
  [params.list]
    # special amount of posts in each list page
    paginate = 15
    # date format (month and day)
    dateFormat = "01-02"
    # amount of RSS pages
    rss = 10

  # Page config
  [params.page]
    # whether to hide a page from home page
    hiddenFromHomePage = true
    # whether to hide a page from search results
    hiddenFromSearch = false
    # whether to enable twemoji
    twemoji = false
    # whether to enable lightgallery
    lightgallery = false
    # whether to enable the ruby extended syntax
    ruby = true
    # whether to enable the fraction extended syntax
    fraction = true
    # whether to enable the fontawesome extended syntax
    fontawesome = true

    # whether to show link to Raw Markdown content of the content
    linkToMarkdown = false
    # configure the link to view source the post
    # linkToSource = "https://github.com/ktuyends/myblog/tree/main/content/{path}"
    # configure the link to edit the post
    # 配置编辑文章的链接
    # linkToEdit = "https://github.com/ktuyends/myblog/tree/main/content/{path}"
    # https://github.com/user/repo/edit/main/{path}
    # https://gitlab.com/user/repo/-/edit/main/{path}
    # https://bitbucket.org/user/repo/src/main/{path}?mode=edit
    # configure the link to report issue the post
    # linkToReport = "https://github.com/ktuyends/myblog/issues/new?title=[bug]%20{title}&body=|Field|Value|%0A|-|-|%0A|Title|{title}|%0A|Url|{url}|%0A|Filename|https://github.com/HEIGE-PCloud/DoIt/blob/main/exampleSite/content/{path}|"
    # https://github.com/user/repo/issues/new?title=[bug]%20{title}&body=|Field|Value|%0A|-|-|%0A|Title|{title}|%0A|Url|{url}|%0A|Filename|https://github.com/user/repo/blob/main/{path}|"
    # https://gitlab.com/user/repo/-/issues/new?issue[title]=[bug]%20{title}&issue[description]=|Field|Value|%0A|-|-|%0A|Title|{title}|%0A|Url|{url}|%0A|Filename|https://gitlab.com/user/repo/-/edit/main/{path}|

    # whether to show the full text content in RSS
    rssFullText = false
    # Page style ("normal", "wide")
    pageStyle = "normal"
    # whether to enable series navigation
    seriesNavigation = true
    # Display a message at the beginning of an article to warn the reader that its content might be outdated.
    [params.page.outdatedArticleReminder]
      enable = true
      # Display the reminder if the last modified time is more than 90 days ago.
      reminder = 90
      # Display warning if the last modified time is more than 180 days ago.
      warning = 180

    # Table of the contents config
    [params.page.toc]
      # whether to enable the table of the contents
      enable = true
      # whether to keep the static table of the contents in front of the post
      keepStatic = false
      # whether to make the table of the contents in the sidebar automatically collapsed
      auto = true

    # Code config
    [params.page.code]
      # whether to show the copy button of the code block
      copy = true
      # the maximum number of lines of displayed code by default
      maxShownLines = 10

    # KaTeX mathematical formulas config (KaTeX https://katex.org/)
    [params.page.math]
      enable = true
      # default block delimiter is $$ ... $$ and \\[ ... \\]
      blockLeftDelimiter = ""
      blockRightDelimiter = ""
      # default inline delimiter is $ ... $ and \\( ... \\)
      inlineLeftDelimiter = ""
      inlineRightDelimiter = ""
      # KaTeX extension copy_tex
      copyTex = true
      # KaTeX extension mhchem
      mhchem = true

    # Mapbox GL JS config (Mapbox GL JS https://docs.mapbox.com/mapbox-gl-js)
    [params.page.mapbox]
      # access token of Mapbox GL JS
      accessToken = "pk.eyJ1IjoiZGlsbG9uenEiLCJhIjoiY2s2czd2M2x3MDA0NjNmcGxmcjVrZmc2cyJ9.aSjv2BNuZUfARvxRYjSVZQ"
      # style for the light theme
      lightStyle = "mapbox://styles/mapbox/light-v10?optimize=true"
      # style for the dark theme
      darkStyle = "mapbox://styles/mapbox/dark-v10?optimize=true"
      # whether to add NavigationControl (https://docs.mapbox.com/mapbox-gl-js/api/#navigationcontrol)
      navigation = true
      # whether to add GeolocateControl (https://docs.mapbox.com/mapbox-gl-js/api/#geolocatecontrol)
      geolocate = true
      # whether to add ScaleControl (https://docs.mapbox.com/mapbox-gl-js/api/#scalecontrol)
      scale = true
      # whether to add FullscreenControl (https://docs.mapbox.com/mapbox-gl-js/api/#fullscreencontrol)
      fullscreen = true

    # Social share links in post page
    [params.page.share]
      enable = true
      Twitter = true
      Facebook = true
      Linkedin = true
      Whatsapp = false
      Pinterest = false
      Tumblr = false
      HackerNews = false
      Reddit = true
      VK = false
      Buffer = false
      Xing = false
      Line = false
      Instapaper = false
      Pocket = false
      Digg = false
      Stumbleupon = false
      Flipboard = false
      Weibo = false
      Renren = false
      Myspace = false
      Blogger = false
      Baidu = false
      Odnoklassniki = false
      Evernote = false
      Skype = false
      Trello = false
      Mix = false
      Telegram = false

    # Comment config
    [params.page.comment]
      enable = true

      # Disqus comment config (https://disqus.com/)
      [params.page.comment.disqus]
        enable = false
        # Disqus shortname to use Disqus in posts
        shortname = ""

      # Gitalk comment config (https://github.com/gitalk/gitalk)
      [params.page.comment.gitalk]
        enable = false
        owner = ""
        repo = ""
        clientId = ""
        clientSecret = ""

      # Valine comment config (https://github.com/xCss/Valine)
      [params.page.comment.valine]
        enable = false
        appId = ""
        appKey = ""
        placeholder = ""
        avatar = "mp"
        meta= ""
        pageSize = 10
        lang = "en"
        visitor = true
        recordIP = false
        highlight = true
        enableQQ = false
        serverURLs = ""
        # emoji data file name, default is "google.yml"
        # ("apple.yml", "google.yml", "facebook.yml", "twitter.yml")
        # located in "themes/DoIt/assets/data/emoji/" directory
        # you can store your own data files in the same path under your project:
        # "assets/data/emoji/"
        # ("apple.yml", "google.yml", "facebook.yml", "twitter.yml")
        # "assets/data/emoji/"
        emoji = ""

      # Waline comment config (https://waline.js.org)
      [params.page.comment.waline]
        enable = false
        serverURL = ""
        visitor = false
        emoji = ['https://cdn.jsdelivr.net/gh/walinejs/emojis/weibo']
        meta = ['nick', 'mail', 'link']
        requiredMeta = []
        login = 'enable'
        wordLimit = 0
        pageSize = 10
        uploadImage = false
        highlight = true
        mathTagSupport = false
        commentCount = false

      # Facebook comment config (https://developers.facebook.com/docs/plugins/comments)
      [params.page.comment.facebook]
        enable = false
        width = "100%"
        numPosts = 10
        appId = ""
        languageCode = ""

      # Telegram comments config (https://comments.app/)
      [params.page.comment.telegram]
        enable = false
        siteID = ""
        limit = 5
        height = ""
        color = ""
        colorful = true
        dislikes = false
        outlined = false
        dark = false

      # Commento comment config (https://commento.io/)
      [params.page.comment.commento]
        enable = false

      # Utterances comment config (https://utteranc.es/)
      [params.page.comment.utterances]
        enable = false
        # owner/repo
        repo = ""
        issueTerm = "pathname"
        label = ""
        lightTheme = "github-light"
        darkTheme = "github-dark"

      # Twikoo comment config (https://twikoo.js.org/)
      [params.page.comment.twikoo]
        enable = false
        envId = ""
        region = ""
        path = ""
        visitor = true
        commentCount = true

      # Vssue comment config (https://vssue.js.org//)
      [params.page.comment.vssue]
        enable = false
        platform = "" # ("bitbucket", "gitea", "gitee", "github", "gitlab")
        owner = ""
        repo = ""
        clientId = ""
        clientSecret = ""

      # Remark42 comment config (https://remark42.com/)
      [params.page.comment.remark42]
        enable = false
        host = ""
        site_id = ""
        max_shown_comments = 15
        show_email_subscription = true
        simple_view = false

      # giscus comment config (https://giscus.app/)
      [params.page.comment.giscus]
        enable = false
        # owner/repo
        dataRepo = ""
        dataRepoId = ""
        dataCategory = ""
        dataCategoryId = ""
        dataMapping = "pathname"
        dataReactionsEnabled = "1"
        dataEmitMetadata = "0"
        lightTheme = "light"
        darkTheme = "dark"

    # Third-party library config
    [params.page.library]
      [params.page.library.css]
        # someCSS = "some.css"
        # located in "assets/"
        # Or
        # someCSS = "https://cdn.example.com/some.css"
      [params.page.library.js]
        # someJavascript = "some.js"
        # located in "assets/"
        # Or
        # someJavascript = "https://cdn.example.com/some.js"

    # Page SEO config
    [params.page.seo]
      # image URL
      # images = []
      # Publisher info
      # [params.page.seo.publisher]
        # name = "xxxx"
        # logoUrl = "/images/avatar.webp"

  # Sponsor config
  [params.sponsor]
    enable = false
    bio = "If you find this post helpful, please consider sponsoring."
    link = "https://github.com/sponsors/ktuyends"
    # custom = "<a href=\"https://www.buymeacoffee.com/ktuyends\" target=\"_blank\"><img src=\"https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png\" alt=\"Buy Me A Coffee\" style=\"height: 40px !important;width: 145 !important;\" ></a>"

  # TypeIt config
  [params.typeit]
    # typing speed between each step (measured in milliseconds)
    speed = 100
    # blinking speed of the cursor (measured in milliseconds)
    cursorSpeed = 1000
    # character used for the cursor (HTML format is supported)
    cursorChar = " "
    # cursor duration after typing finishing (measured in milliseconds, "-1" means unlimited)
    duration = -1

  # Site verification code for Google/Bing/Yandex/Pinterest/Baidu
  [params.verification]
    google = ""
    bing = ""
    yandex = ""
    pinterest = ""
    baidu = ""
    so = ""
    sogou = ""

  # Site SEO config
  [params.seo]
    # image URL
    image = ""
    # thumbnail URL
    thumbnailUrl = ""

  # Analytics config
  [params.analytics]
    enable = false
    # Google Analytics
    [params.analytics.google]
      id = ""
      # whether to anonymize IP
      anonymizeIP = true

    # Fathom Analytics
    [params.analytics.fathom]
      id = ""
      # server url for your tracker if you're self hosting
      server = ""

    # Baidu Analytics
    [params.analytics.baidu]
      id = ""

    # Umami Analytics
    [params.analytics.umami]
      data_website_id = ""
      src = ""
      data_domains = ""

    # Plausible Analytics
    [params.analytics.plausible]
      data_domain = ""
      src = ""

    # Cloudflare Analytics
    [params.analytics.cloudflare]
      token = ""


  # Cookie consent config
  [params.cookieconsent]
    enable = false
    # text strings used for Cookie consent banner
    [params.cookieconsent.content]
      message = ""
      dismiss = ""
      link = ""

  # CDN config for third-party library files
  [params.cdn]
    # CDN data file name, disabled by default
    # ("jsdelivr.yml")
    # located in "themes/DoIt/assets/data/cdn/" directory
    # you can store your own data files in the same path under your project:
    # "assets/data/cdn/"
    data = ""

  # Compatibility config
  [params.compatibility]
    # whether to use Polyfill.io to be compatible with older browsers
    polyfill = false
    # whether to use object-fit-images to be compatible with older browsers
    objectFit = false

# Markup related configuration in Hugo
[markup]
  # Syntax Highlighting (https://gohugo.io/content-management/syntax-highlighting)
  [markup.highlight]
    codeFences = true
    guessSyntax = true
    lineNos = true
    lineNumbersInTable = true
    # false is a necessary configuration (https://github.com/dillonzq/LoveIt/issues/158)
    noClasses = false

  # Goldmark is from Hugo 0.60 the default library used for Markdown
  [markup.goldmark]
    [markup.goldmark.extensions]
      definitionList = true
      footnote = true
      linkify = true
      strikethrough = true
      table = true
      taskList = true
      typographer = true

    [markup.goldmark.renderer]
      # whether to use HTML tags directly in the document
      unsafe = true

  # Table Of Contents settings
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 4

# Author config
[author]
  name = "Tuyen Kieu"
  email = "ktuyen.ds@gmail.com"
  link = "https://github.com/ktuyends"
  avatar = ""
  gravatarEmail = "ktuyen.ds@gmail.com"

# Sitemap config
[sitemap]
  changefreq = "weekly"
  filename = "sitemap.xml"
  priority = 0.5

# Permalinks config (https://gohugo.io/content-management/urls/#permalinks)
[Permalinks]
  # posts = ":year/:month/:filename"
  posts = ":filename"

# Privacy config (https://gohugo.io/about/hugo-and-gdpr/)
[privacy]
  # privacy of the Google Analytics (replaced by params.analytics.google)
  [privacy.googleAnalytics]
    # ...
  [privacy.twitter]
    enableDNT = true
  [privacy.youtube]
    privacyEnhanced = true

# Options to make output .md files
[mediaTypes]
  [mediaTypes."text/plain"]
    suffixes = ["md"]

# Options to make output .md files
[outputFormats.MarkDown]
  mediaType = "text/plain"
  isPlainText = true
  isHTML = false

# Options to make hugo output files
[outputs]
  home = ["HTML", "RSS", "JSON"]
  page = ["HTML", "MarkDown"]
  section = ["HTML", "RSS"]
  taxonomy = ["HTML", "RSS"]
  taxonomyTerm = ["HTML"]

# Options for taxonomies
[taxonomies]
author = "authors"
category = "categories"
tag = "tags"
series = "series"
```

## 3. Viết bài

image: Ảnh cho open graph và twiter

Summary:

- Dùng summary: 
- Dùng Description: Đặt `<!--more-->` ở đầu bài viết 

Math:

$$ c = \pm\sqrt{a^2 + b^2} $$

$$ f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi $$

\$ c = \pm\sqrt{a^2 + b^2} \$ and $f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi$

Fraction: 

[Light]/[Dark]

[99]/[100]

Escape character

```markdown
{?X} -> X
```

\{{< math >}}$\|\boldsymbol{x}\|_{0}=\sqrt[0]{\sum_{i} x_{i}^{0}}${{< /math >}}

Or

{{< math >}}
$$\|\boldsymbol{x}\|_{0}=\sqrt[0]{\sum_{i} x_{i}^{0}}$$
{{< /math >}}

## 4. Markdown

Heading:

```markdown
## h2 Heading {#custom-id}
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading
```

Comments

```markdown
<!--
This is a comment
-->
```

Horizontal Rules

- ---

Format:

```markdown
*rendered as italicized text*
**rendered as bold text**
***bold and italics***
~~Strike through this text.~~

Blockquotes:

```markdown
> something

>> something
```

List:

```markdown
1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
```

```markdown
- Facilisis in pretium nisl aliquet
- Nulla volutpat aliquam velit
    - Phasellus iaculis neque
    - Purus sodales ultricies
```

Task list

```markdown
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

Code

```markdown
In this example, `<section></section>` should be wrapped as **code**.
```

{{< highlight markdown >}}
```markdown
Sample text here...
```
{{< / highlight >}}

Gist

{{< gist spf13 7896402 >}}

Highlight

{{< highlight language >}}
something
{{< /highlight >}}

Table:

| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

Link:

<https://assemble.io>
<contact@revolunet.com>
[Assemble](https://assemble.io)
[Upstage](https://github.com/upstage/ "Visit Upstage!")

Link 2

{{< link "https://assemble.io" >}}


{{< link "mailto:contact@revolunet.com" >}}

{{< link "https://assemble.io" Assemble >}}

{{< link "https://github.com/upstage/" Upstage "Visit Upstage!" >}}

Footnotes

This is a digital footnote[^1].
This is a footnote with "label"[^label]

[^1]: This is a digital footnote
[^label]: This is a footnote with "label"

Image & Figure

![Minion](https://octodex.github.com/images/minion.png)

![Alt text](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")

{{< figure src="/images/lighthouse.webp" title="Lighthouse (figure)" >}}

Notes:

{{< admonition type=notes title="" open=false >}}
some thing
{{< /admonition >}}


Other Shorcodes

{{< tweet 877500564405444608 >}}
{{< vimeo 146022717 >}}
{{< youtube w7Ft2ymGmfc >}}

Showcase

{{< showcase title="Theme Documentation - Basics" summary="Discover what the Hugo - DoIt theme is all about and the core-concepts behind it." image="/theme-documentation-basics/featured-image.webp" link="/theme-documentation-basics" >}}

{{< showcase title="Theme Documentation - Content" summary="Find out how to create and organize your content quickly and intuitively in DoIt theme." image="/theme-documentation-content/featured-image.webp" link="/theme-documentation-content" column="3" >}}

Reference

Bài viết này cũng như vậy, tôi tóm tắt lại một số nội dung trong quyển sách *bookdown: Authoring Books and Technical Documents with R Markdown* của [@bookdown2016].

## 6. Emoji

Theme DoIt hỗ trợ chúng ta chèn một số Emoji vào trong bài viết. Cú pháp:

```markdown
:emoji_code:
```

### Face Smiling

| icon | code | icon | code |
| :-: | - | :-: | - |
| :grinning: | `grinning` | :smiley: | `smiley` |
| :smile: | `smile` | :grin: | `grin` |
| :laughing: | `laughing` <br /> `satisfied` | :sweat_smile: | `sweat_smile` |
| :rofl: | `rofl` | :joy: | `joy` |
| :slightly_smiling_face: | `slightly_smiling_face` | :upside_down_face: | `upside_down_face` |
| :wink: | `wink` | :blush: | `blush` |
| :innocent: | `innocent` | | |

### Face Affection

| icon | code | icon | code |
| :-: | - | :-: | - |
| :heart_eyes: | `heart_eyes` | :kissing_heart: | `kissing_heart` |
| :kissing: | `kissing` | :relaxed: | `relaxed` |
| :kissing_closed_eyes: | `kissing_closed_eyes` | :kissing_smiling_eyes: | `kissing_smiling_eyes` |

### Face Tongue

| icon | code | icon | code |
| :-: | - | :-: | - |
| :yum: | `yum` | :stuck_out_tongue: | `stuck_out_tongue` |
| :stuck_out_tongue_winking_eye: | `stuck_out_tongue_winking_eye` | :stuck_out_tongue_closed_eyes: | `stuck_out_tongue_closed_eyes` |
| :money_mouth_face: | `money_mouth_face` | | |

### Face Hand

| icon | code | icon | code |
| :-: | - | :-: | - |
| :hugs: | `hugs` | :thinking: | `thinking` |

### Face Neutral Skeptical

| icon | code | icon | code |
| :-: | - | :-: | - |
| :zipper_mouth_face: | `zipper_mouth_face` | :neutral_face: | `neutral_face` |
| :expressionless: | `expressionless` | :no_mouth: | `no_mouth` |
| :smirk: | `smirk` | :unamused: | `unamused` |
| :roll_eyes: | `roll_eyes` | :grimacing: | `grimacing` |
| :lying_face: | `lying_face` | | |

### Face Sleepy

| icon | code | icon | code |
| :-: | - | :-: | - |
| :relieved: | `relieved` | :pensive: | `pensive` |
| :sleepy: | `sleepy` | :drooling_face: | `drooling_face` |
| :sleeping: | `sleeping` | | |

### Face Unwell

| icon | code | icon | code |
| :-: | - | :-: | - |
| :mask: | `mask` | :face_with_thermometer: | `face_with_thermometer` |
| :face_with_head_bandage: | `face_with_head_bandage` | :nauseated_face: | `nauseated_face` |
| :sneezing_face: | `sneezing_face` | :dizzy_face: | `dizzy_face` |

### Face Hat

| icon | code | icon | code |
| :-: | - | :-: | - |
| :cowboy_hat_face: | `cowboy_hat_face` | | |

### Face Glasses

| icon | code | icon | code |
| :-: | - | :-: | - |
| :sunglasses: | `sunglasses` | :nerd_face: | `nerd_face` |

### Face Concerned

| icon | code | icon | code |
| :-: | - | :-: | - |
| :confused: | `confused` | :worried: | `worried` |
| :slightly_frowning_face: | `slightly_frowning_face` | :frowning_face: | `frowning_face` |
| :open_mouth: | `open_mouth` | :hushed: | `hushed` |
| :astonished: | `astonished` | :flushed: | `flushed` |
| :frowning: | `frowning` | :anguished: | `anguished` |
| :fearful: | `fearful` | :cold_sweat: | `cold_sweat` |
| :disappointed_relieved: | `disappointed_relieved` | :cry: | `cry` |
| :sob: | `sob` | :scream: | `scream` |
| :confounded: | `confounded` | :persevere: | `persevere` |
| :disappointed: | `disappointed` | :sweat: | `sweat` |
| :weary: | `weary` | :tired_face: | `tired_face` |

### Face Negative

| icon | code | icon | code |
| :-: | - | :-: | - |
| :triumph: | `triumph` | :pout: | `pout` <br /> `rage` |
| :angry: | `angry` | :smiling_imp: | `smiling_imp` |
| :imp: | `imp` | :skull: | `skull` |
| :skull_and_crossbones: | `skull_and_crossbones` | | |

### Face Costume

| icon | code | icon | code |
| :-: | - | :-: | - |
| :hankey: | `hankey` <br /> `poop` <br /> `shit` | :clown_face: | `clown_face` |
| :japanese_ogre: | `japanese_ogre` | :japanese_goblin: | `japanese_goblin` |
| :ghost: | `ghost` | :alien: | `alien` |
| :space_invader: | `space_invader` | :robot: | `robot` |

### Cat Face

| icon | code | icon | code |
| :-: | - | :-: | - |
| :smiley_cat: | `smiley_cat` | :smile_cat: | `smile_cat` |
| :joy_cat: | `joy_cat` | :heart_eyes_cat: | `heart_eyes_cat` |
| :smirk_cat: | `smirk_cat` | :kissing_cat: | `kissing_cat` |
| :scream_cat: | `scream_cat` | :crying_cat_face: | `crying_cat_face` |
| :pouting_cat: | `pouting_cat` | | |

### Monkey Face

| icon | code | icon | code |
| :-: | - | :-: | - |
| :see_no_evil: | `see_no_evil` | :hear_no_evil: | `hear_no_evil` |
| :speak_no_evil: | `speak_no_evil` | | |

### Emotion

| icon | code | icon | code |
| :-: | - | :-: | - |
| :kiss: | `kiss` | :love_letter: | `love_letter` |
| :cupid: | `cupid` | :gift_heart: | `gift_heart` |
| :sparkling_heart: | `sparkling_heart` | :heartpulse: | `heartpulse` |
| :heartbeat: | `heartbeat` | :revolving_hearts: | `revolving_hearts` |
| :two_hearts: | `two_hearts` | :heart_decoration: | `heart_decoration` |
| :heavy_heart_exclamation: | `heavy_heart_exclamation` | :broken_heart: | `broken_heart` |
| :heart: | `heart` | :yellow_heart: | `yellow_heart` |
| :green_heart: | `green_heart` | :blue_heart: | `blue_heart` |
| :purple_heart: | `purple_heart` | :black_heart: | `black_heart` |
| :100: | `100` | :anger: | `anger` |
| :boom: | `boom` <br /> `collision` | :dizzy: | `dizzy` |
| :sweat_drops: | `sweat_drops` | :dash: | `dash` |
| :hole: | `hole` | :bomb: | `bomb` |
| :speech_balloon: | `speech_balloon` | :eye_speech_bubble: | `eye_speech_bubble` |
| :right_anger_bubble: | `right_anger_bubble` | :thought_balloon: | `thought_balloon` |
| :zzz: | `zzz` | | |

### Hand Fingers Open

| icon | code | icon | code |
| :-: | - | :-: | - |
| :wave: | `wave` | :raised_back_of_hand: | `raised_back_of_hand` |
| :raised_hand_with_fingers_splayed: | `raised_hand_with_fingers_splayed` | :hand: | `hand` <br /> `raised_hand` |
| :vulcan_salute: | `vulcan_salute` | | |

### Hand Fingers Partial

| icon | code | icon | code |
| :-: | - | :-: | - |
| :ok_hand: | `ok_hand` | :v: | `v` |
| :crossed_fingers: | `crossed_fingers` | :metal: | `metal` |
| :call_me_hand: | `call_me_hand` | | |

### Hand Single Finger

| icon | code | icon | code |
| :-: | - | :-: | - |
| :point_left: | `point_left` | :point_right: | `point_right` |
| :point_up_2: | `point_up_2` | :fu: | `fu` <br /> `middle_finger` |
| :point_down: | `point_down` | :point_up: | `point_up` |

### Hand Fingers Closed

| icon | code | icon | code |
| :-: | - | :-: | - |
| :+1: | `+1` <br /> `thumbsup` | :-1: | `-1` <br /> `thumbsdown` |
| :fist: | `fist` <br /> `fist_raised` | :facepunch: | `facepunch` <br /> `fist_oncoming` <br /> `punch` |
| :fist_left: | `fist_left` | :fist_right: | `fist_right` |

### Hands

| icon | code | icon | code |
| :-: | - | :-: | - |
| :clap: | `clap` | :raised_hands: | `raised_hands` |
| :open_hands: | `open_hands` | :handshake: | `handshake` |
| :pray: | `pray` | | |

### Hand Prop

| icon | code | icon | code |
| :-: | - | :-: | - |
| :writing_hand: | `writing_hand` | :nail_care: | `nail_care` |
| :selfie: | `selfie` | | |

### Body Parts

| icon | code | icon | code |
| :-: | - | :-: | - |
| :muscle: | `muscle` | :ear: | `ear` |
| :nose: | `nose` | :eyes: | `eyes` |
| :eye: | `eye` | :tongue: | `tongue` |
| :lips: | `lips` | | |

### Person

| icon | code | icon | code |
| :-: | - | :-: | - |
| :baby: | `baby` | :boy: | `boy` |
| :girl: | `girl` | :blonde_man: | `blonde_man` <br /> `person_with_blond_hair` |
| :man: | `man` | :woman: | `woman` |
| :blonde_woman: | `blonde_woman` | :older_man: | `older_man` |
| :older_woman: | `older_woman` | | |

### Person Gesture

| icon | code | icon | code |
| :-: | - | :-: | - |
| :frowning_woman: | `frowning_woman` <br /> `person_frowning` | :frowning_man: | `frowning_man` |
| :person_with_pouting_face: | `person_with_pouting_face` <br /> `pouting_woman` | :pouting_man: | `pouting_man` |
| :ng_woman: | `ng_woman` <br /> `no_good` <br /> `no_good_woman` | :ng_man: | `ng_man` <br /> `no_good_man` |
| :ok_woman: | `ok_woman` | :ok_man: | `ok_man` |
| :information_desk_person: | `information_desk_person` <br /> `sassy_woman` <br /> `tipping_hand_woman` | :sassy_man: | `sassy_man` <br /> `tipping_hand_man` |
| :raising_hand: | `raising_hand` <br /> `raising_hand_woman` | :raising_hand_man: | `raising_hand_man` |
| :bow: | `bow` <br /> `bowing_man` | :bowing_woman: | `bowing_woman` |
| :man_facepalming: | `man_facepalming` | :woman_facepalming: | `woman_facepalming` |
| :man_shrugging: | `man_shrugging` | :woman_shrugging: | `woman_shrugging` |

### Person Role

| icon | code | icon | code |
| :-: | - | :-: | - |
| :man_health_worker: | `man_health_worker` | :woman_health_worker: | `woman_health_worker` |
| :man_student: | `man_student` | :woman_student: | `woman_student` |
| :man_teacher: | `man_teacher` | :woman_teacher: | `woman_teacher` |
| :man_judge: | `man_judge` | :woman_judge: | `woman_judge` |
| :man_farmer: | `man_farmer` | :woman_farmer: | `woman_farmer` |
| :man_cook: | `man_cook` | :woman_cook: | `woman_cook` |
| :man_mechanic: | `man_mechanic` | :woman_mechanic: | `woman_mechanic` |
| :man_factory_worker: | `man_factory_worker` | :woman_factory_worker: | `woman_factory_worker` |
| :man_office_worker: | `man_office_worker` | :woman_office_worker: | `woman_office_worker` |
| :man_scientist: | `man_scientist` | :woman_scientist: | `woman_scientist` |
| :man_technologist: | `man_technologist` | :woman_technologist: | `woman_technologist` |
| :man_singer: | `man_singer` | :woman_singer: | `woman_singer` |
| :man_artist: | `man_artist` | :woman_artist: | `woman_artist` |
| :man_pilot: | `man_pilot` | :woman_pilot: | `woman_pilot` |
| :man_astronaut: | `man_astronaut` | :woman_astronaut: | `woman_astronaut` |
| :man_firefighter: | `man_firefighter` | :woman_firefighter: | `woman_firefighter` |
| :cop: | `cop` <br /> `policeman` | :policewoman: | `policewoman` |
| :detective: | `detective` <br /> `male_detective` | :female_detective: | `female_detective` |
| :guardsman: | `guardsman` | :guardswoman: | `guardswoman` |
| :construction_worker: | `construction_worker` <br /> `construction_worker_man` | :construction_worker_woman: | `construction_worker_woman` |
| :prince: | `prince` | :princess: | `princess` |
| :man_with_turban: | `man_with_turban` | :woman_with_turban: | `woman_with_turban` |
| :man_with_gua_pi_mao: | `man_with_gua_pi_mao` | :man_in_tuxedo: | `man_in_tuxedo` |
| :bride_with_veil: | `bride_with_veil` | :pregnant_woman: | `pregnant_woman` |

### Person Fantasy

| icon | code | icon | code |
| :-: | - | :-: | - |
| :angel: | `angel` | :santa: | `santa` |
| :mrs_claus: | `mrs_claus` | | |

### Person Activity

| icon | code | icon | code |
| :-: | - | :-: | - |
| :massage: | `massage` <br /> `massage_woman` | :massage_man: | `massage_man` |
| :haircut: | `haircut` <br /> `haircut_woman` | :haircut_man: | `haircut_man` |
| :walking: | `walking` <br /> `walking_man` | :walking_woman: | `walking_woman` |
| :runner: | `runner` <br /> `running` <br /> `running_man` | :running_woman: | `running_woman` |
| :dancer: | `dancer` | :man_dancing: | `man_dancing` |
| :business_suit_levitating: | `business_suit_levitating` | :dancers: | `dancers` <br /> `dancing_women` |
| :dancing_men: | `dancing_men` | | |

### Person Sport

| icon | code | icon | code |
| :-: | - | :-: | - |
| :person_fencing: | `person_fencing` | :horse_racing: | `horse_racing` |
| :skier: | `skier` | :snowboarder: | `snowboarder` |
| :golfing_man: | `golfing_man` | :golfing_woman: | `golfing_woman` |
| :surfer: | `surfer` <br /> `surfing_man` | :surfing_woman: | `surfing_woman` |
| :rowboat: | `rowboat` <br /> `rowing_man` | :rowing_woman: | `rowing_woman` |
| :swimmer: | `swimmer` <br /> `swimming_man` | :swimming_woman: | `swimming_woman` |
| :basketball_man: | `basketball_man` | :basketball_woman: | `basketball_woman` |
| :weight_lifting_man: | `weight_lifting_man` | :weight_lifting_woman: | `weight_lifting_woman` |
| :bicyclist: | `bicyclist` <br /> `biking_man` | :biking_woman: | `biking_woman` |
| :mountain_bicyclist: | `mountain_bicyclist` <br /> `mountain_biking_man` | :mountain_biking_woman: | `mountain_biking_woman` |
| :man_cartwheeling: | `man_cartwheeling` | :woman_cartwheeling: | `woman_cartwheeling` |
| :men_wrestling: | `men_wrestling` | :women_wrestling: | `women_wrestling` |
| :man_playing_water_polo: | `man_playing_water_polo` | :woman_playing_water_polo: | `woman_playing_water_polo` |
| :man_playing_handball: | `man_playing_handball` | :woman_playing_handball: | `woman_playing_handball` |
| :man_juggling: | `man_juggling` | :woman_juggling: | `woman_juggling` |

### Person Resting

| icon | code | icon | code |
| :-: | - | :-: | - |
| :bath: | `bath` | :sleeping_bed: | `sleeping_bed` |

### Family

| icon | code | icon | code |
| :-: | - | :-: | - |
| :two_women_holding_hands: | `two_women_holding_hands` | :couple: | `couple` |
| :two_men_holding_hands: | `two_men_holding_hands` | :couplekiss_man_woman: | `couplekiss_man_woman` |
| :couplekiss_man_man: | `couplekiss_man_man` | :couplekiss_woman_woman: | `couplekiss_woman_woman` |
| :couple_with_heart: | `couple_with_heart` <br /> `couple_with_heart_woman_man` | :couple_with_heart_man_man: | `couple_with_heart_man_man` |
| :couple_with_heart_woman_woman: | `couple_with_heart_woman_woman` | :family: | `family` <br /> `family_man_woman_boy` |
| :family_man_woman_girl: | `family_man_woman_girl` | :family_man_woman_girl_boy: | `family_man_woman_girl_boy` |
| :family_man_woman_boy_boy: | `family_man_woman_boy_boy` | :family_man_woman_girl_girl: | `family_man_woman_girl_girl` |
| :family_man_man_boy: | `family_man_man_boy` | :family_man_man_girl: | `family_man_man_girl` |
| :family_man_man_girl_boy: | `family_man_man_girl_boy` | :family_man_man_boy_boy: | `family_man_man_boy_boy` |
| :family_man_man_girl_girl: | `family_man_man_girl_girl` | :family_woman_woman_boy: | `family_woman_woman_boy` |
| :family_woman_woman_girl: | `family_woman_woman_girl` | :family_woman_woman_girl_boy: | `family_woman_woman_girl_boy` |
| :family_woman_woman_boy_boy: | `family_woman_woman_boy_boy` | :family_woman_woman_girl_girl: | `family_woman_woman_girl_girl` |
| :family_man_boy: | `family_man_boy` | :family_man_boy_boy: | `family_man_boy_boy` |
| :family_man_girl: | `family_man_girl` | :family_man_girl_boy: | `family_man_girl_boy` |
| :family_man_girl_girl: | `family_man_girl_girl` | :family_woman_boy: | `family_woman_boy` |
| :family_woman_boy_boy: | `family_woman_boy_boy` | :family_woman_girl: | `family_woman_girl` |
| :family_woman_girl_boy: | `family_woman_girl_boy` | :family_woman_girl_girl: | `family_woman_girl_girl` |

### Person Symbol

| icon | code | icon | code |
| :-: | - | :-: | - |
| :speaking_head: | `speaking_head` | :bust_in_silhouette: | `bust_in_silhouette` |
| :busts_in_silhouette: | `busts_in_silhouette` | :footprints: | `footprints` |

### Animal Mammal

| icon | code | icon | code |
| :-: | - | :-: | - |
| :monkey_face: | `monkey_face` | :monkey: | `monkey` |
| :gorilla: | `gorilla` | :dog: | `dog` |
| :dog2: | `dog2` | :poodle: | `poodle` |
| :wolf: | `wolf` | :fox_face: | `fox_face` |
| :cat: | `cat` | :cat2: | `cat2` |
| :lion: | `lion` | :tiger: | `tiger` |
| :tiger2: | `tiger2` | :leopard: | `leopard` |
| :horse: | `horse` | :racehorse: | `racehorse` |
| :unicorn: | `unicorn` | :deer: | `deer` |
| :cow: | `cow` | :ox: | `ox` |
| :water_buffalo: | `water_buffalo` | :cow2: | `cow2` |
| :pig: | `pig` | :pig2: | `pig2` |
| :boar: | `boar` | :pig_nose: | `pig_nose` |
| :ram: | `ram` | :sheep: | `sheep` |
| :goat: | `goat` | :dromedary_camel: | `dromedary_camel` |
| :camel: | `camel` | :elephant: | `elephant` |
| :rhinoceros: | `rhinoceros` | :mouse: | `mouse` |
| :mouse2: | `mouse2` | :rat: | `rat` |
| :hamster: | `hamster` | :rabbit: | `rabbit` |
| :rabbit2: | `rabbit2` | :chipmunk: | `chipmunk` |
| :bat: | `bat` | :bear: | `bear` |
| :koala: | `koala` | :panda_face: | `panda_face` |
| :feet: | `feet` <br /> `paw_prints` | | |

### Animal Bird

| icon | code | icon | code |
| :-: | - | :-: | - |
| :turkey: | `turkey` | :chicken: | `chicken` |
| :rooster: | `rooster` | :hatching_chick: | `hatching_chick` |
| :baby_chick: | `baby_chick` | :hatched_chick: | `hatched_chick` |
| :bird: | `bird` | :penguin: | `penguin` |
| :dove: | `dove` | :eagle: | `eagle` |
| :duck: | `duck` | :owl: | `owl` |

### Animal Amphibian

| icon | code | icon | code |
| :-: | - | :-: | - |
| :frog: | `frog` |

### Animal Reptile

| icon | code | icon | code |
| :-: | - | :-: | - |
| :crocodile: | `crocodile` | :turtle: | `turtle` |
| :lizard: | `lizard` | :snake: | `snake` |
| :dragon_face: | `dragon_face` | :dragon: | `dragon` |

### Animal Marine

| icon | code | icon | code |
| :-: | - | :-: | - |
| :whale: | `whale` | :whale2: | `whale2` |
| :dolphin: | `dolphin` <br /> `flipper` | :fish: | `fish` |
| :tropical_fish: | `tropical_fish` | :blowfish: | `blowfish` |
| :shark: | `shark` | :octopus: | `octopus` |
| :shell: | `shell` | | |

### Animal Bug

| icon | code | icon | code |
| :-: | - | :-: | - |
| :snail: | `snail` | :butterfly: | `butterfly` |
| :bug: | `bug` | :ant: | `ant` |
| :bee: | `bee` <br /> `honeybee` | :beetle: | `beetle` |
| :spider: | `spider` | :spider_web: | `spider_web` |
| :scorpion: | `scorpion` | | |

### Plant Flower

| icon | code | icon | code |
| :-: | - | :-: | - |
| :bouquet: | `bouquet` | :cherry_blossom: | `cherry_blossom` |
| :white_flower: | `white_flower` | :rosette: | `rosette` |
| :rose: | `rose` | :wilted_flower: | `wilted_flower` |
| :hibiscus: | `hibiscus` | :sunflower: | `sunflower` |
| :blossom: | `blossom` | :tulip: | `tulip` |

### Plant Other

| icon | code | icon | code |
| :-: | - | :-: | - |
| :seedling: | `seedling` | :evergreen_tree: | `evergreen_tree` |
| :deciduous_tree: | `deciduous_tree` | :palm_tree: | `palm_tree` |
| :cactus: | `cactus` | :ear_of_rice: | `ear_of_rice` |
| :herb: | `herb` | :shamrock: | `shamrock` |
| :four_leaf_clover: | `four_leaf_clover` | :maple_leaf: | `maple_leaf` |
| :fallen_leaf: | `fallen_leaf` | :leaves: | `leaves` |

### Food Fruit

| icon | code | icon | code |
| :-: | - | :-: | - |
| :grapes: | `grapes` | :melon: | `melon` |
| :watermelon: | `watermelon` | :mandarin: | `mandarin` <br /> `orange` <br /> `tangerine` |
| :lemon: | `lemon` | :banana: | `banana` |
| :pineapple: | `pineapple` | :apple: | `apple` |
| :green_apple: | `green_apple` | :pear: | `pear` |
| :peach: | `peach` | :cherries: | `cherries` |
| :strawberry: | `strawberry` | :kiwi_fruit: | `kiwi_fruit` |
| :tomato: | `tomato` | | |

### Food Vegetable

| icon | code | icon | code |
| :-: | - | :-: | - |
| :avocado: | `avocado` | :eggplant: | `eggplant` |
| :potato: | `potato` | :carrot: | `carrot` |
| :corn: | `corn` | :hot_pepper: | `hot_pepper` |
| :cucumber: | `cucumber` | :mushroom: | `mushroom` |
| :peanuts: | `peanuts` | :chestnut: | `chestnut` |

### Food Prepared

| icon | code | icon | code |
| :-: | - | :-: | - |
| :bread: | `bread` | :croissant: | `croissant` |
| :baguette_bread: | `baguette_bread` | :pancakes: | `pancakes` |
| :cheese: | `cheese` | :meat_on_bone: | `meat_on_bone` |
| :poultry_leg: | `poultry_leg` | :bacon: | `bacon` |
| :hamburger: | `hamburger` | :fries: | `fries` |
| :pizza: | `pizza` | :hotdog: | `hotdog` |
| :taco: | `taco` | :burrito: | `burrito` |
| :stuffed_flatbread: | `stuffed_flatbread` | :egg: | `egg` |
| :fried_egg: | `fried_egg` | :shallow_pan_of_food: | `shallow_pan_of_food` |
| :stew: | `stew` | :green_salad: | `green_salad` |
| :popcorn: | `popcorn` | | |

### Food Asian

| icon | code | icon | code |
| :-: | - | :-: | - |
| :bento: | `bento` | :rice_cracker: | `rice_cracker` |
| :rice_ball: | `rice_ball` | :rice: | `rice` |
| :curry: | `curry` | :ramen: | `ramen` |
| :spaghetti: | `spaghetti` | :sweet_potato: | `sweet_potato` |
| :oden: | `oden` | :sushi: | `sushi` |
| :fried_shrimp: | `fried_shrimp` | :fish_cake: | `fish_cake` |
| :dango: | `dango` | | |

### Food Marine

| icon | code | icon | code |
| :-: | - | :-: | - |
| :crab: | `crab` | :shrimp: | `shrimp` |
| :squid: | `squid` | | |

### Food Sweet

| icon | code | icon | code |
| :-: | - | :-: | - |
| :icecream: | `icecream` | :shaved_ice: | `shaved_ice` |
| :ice_cream: | `ice_cream` | :doughnut: | `doughnut` |
| :cookie: | `cookie` | :birthday: | `birthday` |
| :cake: | `cake` | :chocolate_bar: | `chocolate_bar` |
| :candy: | `candy` | :lollipop: | `lollipop` |
| :custard: | `custard` | :honey_pot: | `honey_pot` |

### Drink

| icon | code | icon | code |
| :-: | - | :-: | - |
| :baby_bottle: | `baby_bottle` | :milk_glass: | `milk_glass` |
| :coffee: | `coffee` | :tea: | `tea` |
| :sake: | `sake` | :champagne: | `champagne` |
| :wine_glass: | `wine_glass` | :cocktail: | `cocktail` |
| :tropical_drink: | `tropical_drink` | :beer: | `beer` |
| :beers: | `beers` | :clinking_glasses: | `clinking_glasses` |
| :tumbler_glass: | `tumbler_glass` | | |

### Dishware

| icon | code | icon | code |
| :-: | - | :-: | - |
| :plate_with_cutlery: | `plate_with_cutlery` | :fork_and_knife: | `fork_and_knife` |
| :spoon: | `spoon` | :hocho: | `hocho` <br /> `knife` |
| :amphora: | `amphora` | | |

### Place Map

| icon | code | icon | code |
| :-: | - | :-: | - |
| :earth_africa: | `earth_africa` | :earth_americas: | `earth_americas` |
| :earth_asia: | `earth_asia` | :globe_with_meridians: | `globe_with_meridians` |
| :world_map: | `world_map` | :japan: | `japan` |

### Place Geographic

| icon | code | icon | code |
| :-: | - | :-: | - |
| :mountain_snow: | `mountain_snow` | :mountain: | `mountain` |
| :volcano: | `volcano` | :mount_fuji: | `mount_fuji` |
| :camping: | `camping` | :beach_umbrella: | `beach_umbrella` |
| :desert: | `desert` | :desert_island: | `desert_island` |
| :national_park: | `national_park` | | |

### Place Building

| icon | code | icon | code |
| :-: | - | :-: | - |
| :stadium: | `stadium` | :classical_building: | `classical_building` |
| :building_construction: | `building_construction` | :houses: | `houses` |
| :derelict_house: | `derelict_house` | :house: | `house` |
| :house_with_garden: | `house_with_garden` | :office: | `office` |
| :post_office: | `post_office` | :european_post_office: | `european_post_office` |
| :hospital: | `hospital` | :bank: | `bank` |
| :hotel: | `hotel` | :love_hotel: | `love_hotel` |
| :convenience_store: | `convenience_store` | :school: | `school` |
| :department_store: | `department_store` | :factory: | `factory` |
| :japanese_castle: | `japanese_castle` | :european_castle: | `european_castle` |
| :wedding: | `wedding` | :tokyo_tower: | `tokyo_tower` |
| :statue_of_liberty: | `statue_of_liberty` | | |

### Place Religious

| icon | code | icon | code |
| :-: | - | :-: | - |
| :church: | `church` | :mosque: | `mosque` |
| :synagogue: | `synagogue` | :shinto_shrine: | `shinto_shrine` |
| :kaaba: | `kaaba` | | |

### Place Other

| icon | code | icon | code |
| :-: | - | :-: | - |
| :fountain: | `fountain` | :tent: | `tent` |
| :foggy: | `foggy` | :night_with_stars: | `night_with_stars` |
| :cityscape: | `cityscape` | :sunrise_over_mountains: | `sunrise_over_mountains` |
| :sunrise: | `sunrise` | :city_sunset: | `city_sunset` |
| :city_sunrise: | `city_sunrise` | :bridge_at_night: | `bridge_at_night` |
| :hotsprings: | `hotsprings` | :carousel_horse: | `carousel_horse` |
| :ferris_wheel: | `ferris_wheel` | :roller_coaster: | `roller_coaster` |
| :barber: | `barber` | :circus_tent: | `circus_tent` |

### Transport Ground

| icon | code | icon | code |
| :-: | - | :-: | - |
| :steam_locomotive: | `steam_locomotive` | :railway_car: | `railway_car` |
| :bullettrain_side: | `bullettrain_side` | :bullettrain_front: | `bullettrain_front` |
| :train2: | `train2` | :metro: | `metro` |
| :light_rail: | `light_rail` | :station: | `station` |
| :tram: | `tram` | :monorail: | `monorail` |
| :mountain_railway: | `mountain_railway` | :train: | `train` |
| :bus: | `bus` | :oncoming_bus: | `oncoming_bus` |
| :trolleybus: | `trolleybus` | :minibus: | `minibus` |
| :ambulance: | `ambulance` | :fire_engine: | `fire_engine` |
| :police_car: | `police_car` | :oncoming_police_car: | `oncoming_police_car` |
| :taxi: | `taxi` | :oncoming_taxi: | `oncoming_taxi` |
| :car: | `car` <br /> `red_car` | :oncoming_automobile: | `oncoming_automobile` |
| :blue_car: | `blue_car` | :truck: | `truck` |
| :articulated_lorry: | `articulated_lorry` | :tractor: | `tractor` |
| :racing_car: | `racing_car` | :motorcycle: | `motorcycle` |
| :motor_scooter: | `motor_scooter` | :bike: | `bike` |
| :kick_scooter: | `kick_scooter` | :busstop: | `busstop` |
| :motorway: | `motorway` | :railway_track: | `railway_track` |
| :oil_drum: | `oil_drum` | :fuelpump: | `fuelpump` |
| :rotating_light: | `rotating_light` | :traffic_light: | `traffic_light` |
| :vertical_traffic_light: | `vertical_traffic_light` | :stop_sign: | `stop_sign` |
| :construction: | `construction` | | |

### Transport Water

| icon | code | icon | code |
| :-: | - | :-: | - |
| :anchor: | `anchor` | :boat: | `boat` <br /> `sailboat` |
| :canoe: | `canoe` | :speedboat: | `speedboat` |
| :passenger_ship: | `passenger_ship` | :ferry: | `ferry` |
| :motor_boat: | `motor_boat` | :ship: | `ship` |

### Transport Air

| icon | code | icon | code |
| :-: | - | :-: | - |
| :airplane: | `airplane` | :small_airplane: | `small_airplane` |
| :flight_departure: | `flight_departure` | :flight_arrival: | `flight_arrival` |
| :seat: | `seat` | :helicopter: | `helicopter` |
| :suspension_railway: | `suspension_railway` | :mountain_cableway: | `mountain_cableway` |
| :aerial_tramway: | `aerial_tramway` | :artificial_satellite: | `artificial_satellite` |
| :rocket: | `rocket` | | |

### Hotel

| icon | code | icon | code |
| :-: | - | :-: | - |
| :bellhop_bell: | `bellhop_bell` |

### Time

| icon | code | icon | code |
| :-: | - | :-: | - |
| :hourglass: | `hourglass` | :hourglass_flowing_sand: | `hourglass_flowing_sand` |
| :watch: | `watch` | :alarm_clock: | `alarm_clock` |
| :stopwatch: | `stopwatch` | :timer_clock: | `timer_clock` |
| :mantelpiece_clock: | `mantelpiece_clock` | :clock12: | `clock12` |
| :clock1230: | `clock1230` | :clock1: | `clock1` |
| :clock130: | `clock130` | :clock2: | `clock2` |
| :clock230: | `clock230` | :clock3: | `clock3` |
| :clock330: | `clock330` | :clock4: | `clock4` |
| :clock430: | `clock430` | :clock5: | `clock5` |
| :clock530: | `clock530` | :clock6: | `clock6` |
| :clock630: | `clock630` | :clock7: | `clock7` |
| :clock730: | `clock730` | :clock8: | `clock8` |
| :clock830: | `clock830` | :clock9: | `clock9` |
| :clock930: | `clock930` | :clock10: | `clock10` |
| :clock1030: | `clock1030` | :clock11: | `clock11` |
| :clock1130: | `clock1130` | | |

### Sky & Weather

| icon | code | icon | code |
| :-: | - | :-: | - |
| :new_moon: | `new_moon` | :waxing_crescent_moon: | `waxing_crescent_moon` |
| :first_quarter_moon: | `first_quarter_moon` | :moon: | `moon` <br /> `waxing_gibbous_moon` |
| :full_moon: | `full_moon` | :waning_gibbous_moon: | `waning_gibbous_moon` |
| :last_quarter_moon: | `last_quarter_moon` | :waning_crescent_moon: | `waning_crescent_moon` |
| :crescent_moon: | `crescent_moon` | :new_moon_with_face: | `new_moon_with_face` |
| :first_quarter_moon_with_face: | `first_quarter_moon_with_face` | :last_quarter_moon_with_face: | `last_quarter_moon_with_face` |
| :thermometer: | `thermometer` | :sunny: | `sunny` |
| :full_moon_with_face: | `full_moon_with_face` | :sun_with_face: | `sun_with_face` |
| :star: | `star` | :star2: | `star2` |
| :stars: | `stars` | :milky_way: | `milky_way` |
| :cloud: | `cloud` | :partly_sunny: | `partly_sunny` |
| :cloud_with_lightning_and_rain: | `cloud_with_lightning_and_rain` | :sun_behind_small_cloud: | `sun_behind_small_cloud` |
| :sun_behind_large_cloud: | `sun_behind_large_cloud` | :sun_behind_rain_cloud: | `sun_behind_rain_cloud` |
| :cloud_with_rain: | `cloud_with_rain` | :cloud_with_snow: | `cloud_with_snow` |
| :cloud_with_lightning: | `cloud_with_lightning` | :tornado: | `tornado` |
| :fog: | `fog` | :wind_face: | `wind_face` |
| :cyclone: | `cyclone` | :rainbow: | `rainbow` |
| :closed_umbrella: | `closed_umbrella` | :open_umbrella: | `open_umbrella` |
| :umbrella: | `umbrella` | :parasol_on_ground: | `parasol_on_ground` |
| :zap: | `zap` | :snowflake: | `snowflake` |
| :snowman_with_snow: | `snowman_with_snow` | :snowman: | `snowman` |
| :comet: | `comet` | :fire: | `fire` |
| :droplet: | `droplet` | :ocean: | `ocean` |

### Event

| icon | code | icon | code |
| :-: | - | :-: | - |
| :jack_o_lantern: | `jack_o_lantern` | :christmas_tree: | `christmas_tree` |
| :fireworks: | `fireworks` | :sparkler: | `sparkler` |
| :sparkles: | `sparkles` | :balloon: | `balloon` |
| :tada: | `tada` | :confetti_ball: | `confetti_ball` |
| :tanabata_tree: | `tanabata_tree` | :bamboo: | `bamboo` |
| :dolls: | `dolls` | :flags: | `flags` |
| :wind_chime: | `wind_chime` | :rice_scene: | `rice_scene` |
| :ribbon: | `ribbon` | :gift: | `gift` |
| :reminder_ribbon: | `reminder_ribbon` | :tickets: | `tickets` |
| :ticket: | `ticket` | | |

### Award Medal

| icon | code | icon | code |
| :-: | - | :-: | - |
| :medal_military: | `medal_military` | :trophy: | `trophy` |
| :medal_sports: | `medal_sports` | :1st_place_medal: | `1st_place_medal` |
| :2nd_place_medal: | `2nd_place_medal` | :3rd_place_medal: | `3rd_place_medal` |

### Sport

| icon | code | icon | code |
| :-: | - | :-: | - |
| :soccer: | `soccer` | :baseball: | `baseball` |
| :basketball: | `basketball` | :volleyball: | `volleyball` |
| :football: | `football` | :rugby_football: | `rugby_football` |
| :tennis: | `tennis` | :bowling: | `bowling` |
| :cricket: | `cricket` | :field_hockey: | `field_hockey` |
| :ice_hockey: | `ice_hockey` | :ping_pong: | `ping_pong` |
| :badminton: | `badminton` | :boxing_glove: | `boxing_glove` |
| :martial_arts_uniform: | `martial_arts_uniform` | :goal_net: | `goal_net` |
| :golf: | `golf` | :ice_skate: | `ice_skate` |
| :fishing_pole_and_fish: | `fishing_pole_and_fish` | :running_shirt_with_sash: | `running_shirt_with_sash` |
| :ski: | `ski` | | |

### Game

| icon | code | icon | code |
| :-: | - | :-: | - |
| :dart: | `dart` | :8ball: | `8ball` |
| :crystal_ball: | `crystal_ball` | :video_game: | `video_game` |
| :joystick: | `joystick` | :slot_machine: | `slot_machine` |
| :game_die: | `game_die` | :spades: | `spades` |
| :hearts: | `hearts` | :diamonds: | `diamonds` |
| :clubs: | `clubs` | :black_joker: | `black_joker` |
| :mahjong: | `mahjong` | :flower_playing_cards: | `flower_playing_cards` |

### Arts & Crafts

| icon | code | icon | code |
| :-: | - | :-: | - |
| :performing_arts: | `performing_arts` | :framed_picture: | `framed_picture` |
| :art: | `art` | | |

### Clothing

| icon | code | icon | code |
| :-: | - | :-: | - |
| :eyeglasses: | `eyeglasses` | :dark_sunglasses: | `dark_sunglasses` |
| :necktie: | `necktie` | :shirt: | `shirt` <br /> `tshirt` |
| :jeans: | `jeans` | :dress: | `dress` |
| :kimono: | `kimono` | :bikini: | `bikini` |
| :womans_clothes: | `womans_clothes` | :purse: | `purse` |
| :handbag: | `handbag` | :pouch: | `pouch` |
| :shopping: | `shopping` | :school_satchel: | `school_satchel` |
| :mans_shoe: | `mans_shoe` <br /> `shoe` | :athletic_shoe: | `athletic_shoe` |
| :high_heel: | `high_heel` | :sandal: | `sandal` |
| :boot: | `boot` | :crown: | `crown` |
| :womans_hat: | `womans_hat` | :tophat: | `tophat` |
| :mortar_board: | `mortar_board` | :rescue_worker_helmet: | `rescue_worker_helmet` |
| :prayer_beads: | `prayer_beads` | :lipstick: | `lipstick` |
| :ring: | `ring` | :gem: | `gem` |

### Sound

| icon | code | icon | code |
| :-: | - | :-: | - |
| :mute: | `mute` | :speaker: | `speaker` |
| :sound: | `sound` | :loud_sound: | `loud_sound` |
| :loudspeaker: | `loudspeaker` | :mega: | `mega` |
| :postal_horn: | `postal_horn` | :bell: | `bell` |
| :no_bell: | `no_bell` | | |

### Music

| icon | code | icon | code |
| :-: | - | :-: | - |
| :musical_score: | `musical_score` | :musical_note: | `musical_note` |
| :notes: | `notes` | :studio_microphone: | `studio_microphone` |
| :level_slider: | `level_slider` | :control_knobs: | `control_knobs` |
| :microphone: | `microphone` | :headphones: | `headphones` |
| :radio: | `radio` | | |

### Musical Instrument

| icon | code | icon | code |
| :-: | - | :-: | - |
| :saxophone: | `saxophone` | :guitar: | `guitar` |
| :musical_keyboard: | `musical_keyboard` | :trumpet: | `trumpet` |
| :violin: | `violin` | :drum: | `drum` |

### Phone

| icon | code | icon | code |
| :-: | - | :-: | - |
| :iphone: | `iphone` | :calling: | `calling` |
| :phone: | `phone` <br /> `telephone` | :telephone_receiver: | `telephone_receiver` |
| :pager: | `pager` | :fax: | `fax` |

### Computer

| icon | code | icon | code |
| :-: | - | :-: | - |
| :battery: | `battery` | :electric_plug: | `electric_plug` |
| :computer: | `computer` | :desktop_computer: | `desktop_computer` |
| :printer: | `printer` | :keyboard: | `keyboard` |
| :computer_mouse: | `computer_mouse` | :trackball: | `trackball` |
| :minidisc: | `minidisc` | :floppy_disk: | `floppy_disk` |
| :cd: | `cd` | :dvd: | `dvd` |

### Light & Video

| icon | code | icon | code |
| :-: | - | :-: | - |
| :movie_camera: | `movie_camera` | :film_strip: | `film_strip` |
| :film_projector: | `film_projector` | :clapper: | `clapper` |
| :tv: | `tv` | :camera: | `camera` |
| :camera_flash: | `camera_flash` | :video_camera: | `video_camera` |
| :vhs: | `vhs` | :mag: | `mag` |
| :mag_right: | `mag_right` | :candle: | `candle` |
| :bulb: | `bulb` | :flashlight: | `flashlight` |
| :izakaya_lantern: | `izakaya_lantern` <br /> `lantern` | | |

### Book Paper

| icon | code | icon | code |
| :-: | - | :-: | - |
| :notebook_with_decorative_cover: | `notebook_with_decorative_cover` | :closed_book: | `closed_book` |
| :book: | `book` <br /> `open_book` | :green_book: | `green_book` |
| :blue_book: | `blue_book` | :orange_book: | `orange_book` |
| :books: | `books` | :notebook: | `notebook` |
| :ledger: | `ledger` | :page_with_curl: | `page_with_curl` |
| :scroll: | `scroll` | :page_facing_up: | `page_facing_up` |
| :newspaper: | `newspaper` | :newspaper_roll: | `newspaper_roll` |
| :bookmark_tabs: | `bookmark_tabs` | :bookmark: | `bookmark` |
| :label: | `label` | | |

### Money

| icon | code | icon | code |
| :-: | - | :-: | - |
| :moneybag: | `moneybag` | :yen: | `yen` |
| :dollar: | `dollar` | :euro: | `euro` |
| :pound: | `pound` | :money_with_wings: | `money_with_wings` |
| :credit_card: | `credit_card` | :chart: | `chart` |

### Mail

| icon | code | icon | code |
| :-: | - | :-: | - |
| :email: | `email` <br /> `envelope` | :e-mail: | `:e-mail:` |
| :incoming_envelope: | `incoming_envelope` | :envelope_with_arrow: | `envelope_with_arrow` |
| :outbox_tray: | `outbox_tray` | :inbox_tray: | `inbox_tray` |
| :package: | `package` | :mailbox: | `mailbox` |
| :mailbox_closed: | `mailbox_closed` | :mailbox_with_mail: | `mailbox_with_mail` |
| :mailbox_with_no_mail: | `mailbox_with_no_mail` | :postbox: | `postbox` |
| :ballot_box: | `ballot_box` | | |

### Writing

| icon | code | icon | code |
| :-: | - | :-: | - |
| :pencil2: | `pencil2` | :black_nib: | `black_nib` |
| :fountain_pen: | `fountain_pen` | :pen: | `pen` |
| :paintbrush: | `paintbrush` | :crayon: | `crayon` |
| :memo: | `memo` <br /> `pencil` | | |

### Office

| icon | code | icon | code |
| :-: | - | :-: | - |
| :briefcase: | `briefcase` | :file_folder: | `file_folder` |
| :open_file_folder: | `open_file_folder` | :card_index_dividers: | `card_index_dividers` |
| :date: | `date` | :calendar: | `calendar` |
| :spiral_notepad: | `spiral_notepad` | :spiral_calendar: | `spiral_calendar` |
| :card_index: | `card_index` | :chart_with_upwards_trend: | `chart_with_upwards_trend` |
| :chart_with_downwards_trend: | `chart_with_downwards_trend` | :bar_chart: | `bar_chart` |
| :clipboard: | `clipboard` | :pushpin: | `pushpin` |
| :round_pushpin: | `round_pushpin` | :paperclip: | `paperclip` |
| :paperclips: | `paperclips` | :straight_ruler: | `straight_ruler` |
| :triangular_ruler: | `triangular_ruler` | :scissors: | `scissors` |
| :card_file_box: | `card_file_box` | :file_cabinet: | `file_cabinet` |
| :wastebasket: | `wastebasket` | | |

### Lock

| icon | code | icon | code |
| :-: | - | :-: | - |
| :lock: | `lock` | :unlock: | `unlock` |
| :lock_with_ink_pen: | `lock_with_ink_pen` | :closed_lock_with_key: | `closed_lock_with_key` |
| :key: | `key` | :old_key: | `old_key` |

### Tool

| icon | code | icon | code |
| :-: | - | :-: | - |
| :hammer: | `hammer` | :pick: | `pick` |
| :hammer_and_pick: | `hammer_and_pick` | :hammer_and_wrench: | `hammer_and_wrench` |
| :dagger: | `dagger` | :crossed_swords: | `crossed_swords` |
| :gun: | `gun` | :bow_and_arrow: | `bow_and_arrow` |
| :shield: | `shield` | :wrench: | `wrench` |
| :nut_and_bolt: | `nut_and_bolt` | :gear: | `gear` |
| :clamp: | `clamp` | :balance_scale: | `balance_scale` |
| :link: | `link` | :chains: | `chains` |

### Science

| icon | code | icon | code |
| :-: | - | :-: | - |
| :alembic: | `alembic` | :microscope: | `microscope` |
| :telescope: | `telescope` | :satellite: | `satellite` |

### Medical

| icon | code | icon | code |
| :-: | - | :-: | - |
| :syringe: | `syringe` | :pill: | `pill` |

### Household

| icon | code | icon | code |
| :-: | - | :-: | - |
| :door: | `door` | :bed: | `bed` |
| :couch_and_lamp: | `couch_and_lamp` | :toilet: | `toilet` |
| :shower: | `shower` | :bathtub: | `bathtub` |
| :shopping_cart: | `shopping_cart` | | |

### Other Object

| icon | code | icon | code |
| :-: | - | :-: | - |
| :smoking: | `smoking` | :coffin: | `coffin` |
| :funeral_urn: | `funeral_urn` | :moyai: | `moyai` |

### Transport Sign

| icon | code | icon | code |
| :-: | - | :-: | - |
| :atm: | `atm` | :put_litter_in_its_place: | `put_litter_in_its_place` |
| :potable_water: | `potable_water` | :wheelchair: | `wheelchair` |
| :mens: | `mens` | :womens: | `womens` |
| :restroom: | `restroom` | :baby_symbol: | `baby_symbol` |
| :wc: | `wc` | :passport_control: | `passport_control` |
| :customs: | `customs` | :baggage_claim: | `baggage_claim` |
| :left_luggage: | `left_luggage` | | |

### Warning

| icon | code | icon | code |
| :-: | - | :-: | - |
| :warning: | `warning` | :children_crossing: | `children_crossing` |
| :no_entry: | `no_entry` | :no_entry_sign: | `no_entry_sign` |
| :no_bicycles: | `no_bicycles` | :no_smoking: | `no_smoking` |
| :do_not_litter: | `do_not_litter` | :non-potable_water: | `:non-potable_water:` |
| :no_pedestrians: | `no_pedestrians` | :no_mobile_phones: | `no_mobile_phones` |
| :underage: | `underage` | :radioactive: | `radioactive` |
| :biohazard: | `biohazard` | | |

### Arrow

| icon | code | icon | code |
| :-: | - | :-: | - |
| :arrow_up: | `arrow_up` | :arrow_upper_right: | `arrow_upper_right` |
| :arrow_right: | `arrow_right` | :arrow_lower_right: | `arrow_lower_right` |
| :arrow_down: | `arrow_down` | :arrow_lower_left: | `arrow_lower_left` |
| :arrow_left: | `arrow_left` | :arrow_upper_left: | `arrow_upper_left` |
| :arrow_up_down: | `arrow_up_down` | :left_right_arrow: | `left_right_arrow` |
| :leftwards_arrow_with_hook: | `leftwards_arrow_with_hook` | :arrow_right_hook: | `arrow_right_hook` |
| :arrow_heading_up: | `arrow_heading_up` | :arrow_heading_down: | `arrow_heading_down` |
| :arrows_clockwise: | `arrows_clockwise` | :arrows_counterclockwise: | `arrows_counterclockwise` |
| :back: | `back` | :end: | `end` |
| :on: | `on` | :soon: | `soon` |
| :top: | `top` | | |

### Religion

| icon | code | icon | code |
| :-: | - | :-: | - |
| :place_of_worship: | `place_of_worship` | :atom_symbol: | `atom_symbol` |
| :om: | `om` | :star_of_david: | `star_of_david` |
| :wheel_of_dharma: | `wheel_of_dharma` | :yin_yang: | `yin_yang` |
| :latin_cross: | `latin_cross` | :orthodox_cross: | `orthodox_cross` |
| :star_and_crescent: | `star_and_crescent` | :peace_symbol: | `peace_symbol` |
| :menorah: | `menorah` | :six_pointed_star: | `six_pointed_star` |

### Zodiac

| icon | code | icon | code |
| :-: | - | :-: | - |
| :aries: | `aries` | :taurus: | `taurus` |
| :gemini: | `gemini` | :cancer: | `cancer` |
| :leo: | `leo` | :virgo: | `virgo` |
| :libra: | `libra` | :scorpius: | `scorpius` |
| :sagittarius: | `sagittarius` | :capricorn: | `capricorn` |
| :aquarius: | `aquarius` | :pisces: | `pisces` |
| :ophiuchus: | `ophiuchus` | | |

### Av Symbol

| icon | code | icon | code |
| :-: | - | :-: | - |
| :twisted_rightwards_arrows: | `twisted_rightwards_arrows` | :repeat: | `repeat` |
| :repeat_one: | `repeat_one` | :arrow_forward: | `arrow_forward` |
| :fast_forward: | `fast_forward` | :next_track_button: | `next_track_button` |
| :play_or_pause_button: | `play_or_pause_button` | :arrow_backward: | `arrow_backward` |
| :rewind: | `rewind` | :previous_track_button: | `previous_track_button` |
| :arrow_up_small: | `arrow_up_small` | :arrow_double_up: | `arrow_double_up` |
| :arrow_down_small: | `arrow_down_small` | :arrow_double_down: | `arrow_double_down` |
| :pause_button: | `pause_button` | :stop_button: | `stop_button` |
| :record_button: | `record_button` | :cinema: | `cinema` |
| :low_brightness: | `low_brightness` | :high_brightness: | `high_brightness` |
| :signal_strength: | `signal_strength` | :vibration_mode: | `vibration_mode` |
| :mobile_phone_off: | `mobile_phone_off` | | |

### Math

| icon | code | icon | code |
| :-: | - | :-: | - |
| :heavy_multiplication_x: | `heavy_multiplication_x` | :heavy_plus_sign: | `heavy_plus_sign` |
| :heavy_minus_sign: | `heavy_minus_sign` | :heavy_division_sign: | `heavy_division_sign` |

### Punctuation

| icon | code | icon | code |
| :-: | - | :-: | - |
| :bangbang: | `bangbang` | :interrobang: | `interrobang` |
| :question: | `question` | :grey_question: | `grey_question` |
| :grey_exclamation: | `grey_exclamation` | :exclamation: | `exclamation` <br /> `heavy_exclamation_mark` |
| :wavy_dash: | `wavy_dash` | | |

### Currency

| icon | code | icon | code |
| :-: | - | :-: | - |
| :currency_exchange: | `currency_exchange` | :heavy_dollar_sign: | `heavy_dollar_sign` |

### Keycap

| icon | code | icon | code |
| :-: | - | :-: | - |
| :hash: | `hash` | :asterisk: | `asterisk` |
| :zero: | `zero` | :one: | `one` |
| :two: | `two` | :three: | `three` |
| :four: | `four` | :five: | `five` |
| :six: | `six` | :seven: | `seven` |
| :eight: | `eight` | :nine: | `nine` |
| :keycap_ten: | `keycap_ten` | | |

### Alphabet

| icon | code | icon | code |
| :-: | - | :-: | - |
| :capital_abcd: | `capital_abcd` | :abcd: | `abcd` |
| :1234: | `1234` | :symbols: | `symbols` |
| :abc: | `abc` | :a: | `a` |
| :ab: | `ab` | :b: | `b` |
| :cl: | `cl` | :cool: | `cool` |
| :free: | `free` | :information_source: | `information_source` |
| :id: | `id` | :m: | `m` |
| :new: | `new` | :ng: | `ng` |
| :o2: | `o2` | :ok: | `ok` |
| :parking: | `parking` | :sos: | `sos` |
| :up: | `up` | :vs: | `vs` |
| :koko: | `koko` | :sa: | `sa` |
| :u6708: | `u6708` | :u6709: | `u6709` |
| :u6307: | `u6307` | :ideograph_advantage: | `ideograph_advantage` |
| :u5272: | `u5272` | :u7121: | `u7121` |
| :u7981: | `u7981` | :accept: | `accept` |
| :u7533: | `u7533` | :u5408: | `u5408` |
| :u7a7a: | `u7a7a` | :congratulations: | `congratulations` |
| :secret: | `secret` | :u55b6: | `u55b6` |
| :u6e80: | `u6e80` | | |

### Geometric

| icon | code | icon | code |
| :-: | - | :-: | - |
| :red_circle: | `red_circle` | :large_blue_circle: | `large_blue_circle` |
| :black_circle: | `black_circle` | :white_circle: | `white_circle` |
| :black_large_square: | `black_large_square` | :white_large_square: | `white_large_square` |
| :black_medium_square: | `black_medium_square` | :white_medium_square: | `white_medium_square` |
| :black_medium_small_square: | `black_medium_small_square` | :white_medium_small_square: | `white_medium_small_square` |
| :black_small_square: | `black_small_square` | :white_small_square: | `white_small_square` |
| :large_orange_diamond: | `large_orange_diamond` | :large_blue_diamond: | `large_blue_diamond` |
| :small_orange_diamond: | `small_orange_diamond` | :small_blue_diamond: | `small_blue_diamond` |
| :small_red_triangle: | `small_red_triangle` | :small_red_triangle_down: | `small_red_triangle_down` |
| :diamond_shape_with_a_dot_inside: | `diamond_shape_with_a_dot_inside` | :radio_button: | `radio_button` |
| :white_square_button: | `white_square_button` | :black_square_button: | `black_square_button` |

### Other Symbol

| icon | code | icon | code |
| :-: | - | :-: | - |
| :recycle: | `recycle` | :fleur_de_lis: | `fleur_de_lis` |
| :trident: | `trident` | :name_badge: | `name_badge` |
| :beginner: | `beginner` | :o: | `o` |
| :white_check_mark: | `white_check_mark` | :ballot_box_with_check: | `ballot_box_with_check` |
| :heavy_check_mark: | `heavy_check_mark` | :x: | `x` |
| :negative_squared_cross_mark: | `negative_squared_cross_mark` | :curly_loop: | `curly_loop` |
| :loop: | `loop` | :part_alternation_mark: | `part_alternation_mark` |
| :eight_spoked_asterisk: | `eight_spoked_asterisk` | :eight_pointed_black_star: | `eight_pointed_black_star` |
| :sparkle: | `sparkle` | :copyright: | `copyright` |
| :registered: | `registered` | :tm: | `tm` |

### Common Flags

| icon | code | icon | code |
| :-: | - | :-: | - |
| :checkered_flag: | `checkered_flag` | :triangular_flag_on_post: | `triangular_flag_on_post` |
| :crossed_flags: | `crossed_flags` | :black_flag: | `black_flag` |
| :white_flag: | `white_flag` | :rainbow_flag: | `rainbow_flag` |

### Country and Region Flags

| icon | code | icon | code |
| :-: | - | :-: | - |
| :andorra: | `andorra` | :united_arab_emirates: | `united_arab_emirates` |
| :afghanistan: | `afghanistan` | :antigua_barbuda: | `antigua_barbuda` |
| :anguilla: | `anguilla` | :albania: | `albania` |
| :armenia: | `armenia` | :angola: | `angola` |
| :antarctica: | `antarctica` | :argentina: | `argentina` |
| :american_samoa: | `american_samoa` | :austria: | `austria` |
| :australia: | `australia` | :aruba: | `aruba` |
| :aland_islands: | `aland_islands` | :azerbaijan: | `azerbaijan` |
| :bosnia_herzegovina: | `bosnia_herzegovina` | :barbados: | `barbados` |
| :bangladesh: | `bangladesh` | :belgium: | `belgium` |
| :burkina_faso: | `burkina_faso` | :bulgaria: | `bulgaria` |
| :bahrain: | `bahrain` | :burundi: | `burundi` |
| :benin: | `benin` | :st_barthelemy: | `st_barthelemy` |
| :bermuda: | `bermuda` | :brunei: | `brunei` |
| :bolivia: | `bolivia` | :caribbean_netherlands: | `caribbean_netherlands` |
| :brazil: | `brazil` | :bahamas: | `bahamas` |
| :bhutan: | `bhutan` | :botswana: | `botswana` |
| :belarus: | `belarus` | :belize: | `belize` |
| :canada: | `canada` | :cocos_islands: | `cocos_islands` |
| :congo_kinshasa: | `congo_kinshasa` | :central_african_republic: | `central_african_republic` |
| :congo_brazzaville: | `congo_brazzaville` | :switzerland: | `switzerland` |
| :cote_divoire: | `cote_divoire` | :cook_islands: | `cook_islands` |
| :chile: | `chile` | :cameroon: | `cameroon` |
| :cn: | `cn` | :colombia: | `colombia` |
| :costa_rica: | `costa_rica` | :cuba: | `cuba` |
| :cape_verde: | `cape_verde` | :curacao: | `curacao` |
| :christmas_island: | `christmas_island` | :cyprus: | `cyprus` |
| :czech_republic: | `czech_republic` | :de: | `de` |
| :djibouti: | `djibouti` | :denmark: | `denmark` |
| :dominica: | `dominica` | :dominican_republic: | `dominican_republic` |
| :algeria: | `algeria` | :ecuador: | `ecuador` |
| :estonia: | `estonia` | :egypt: | `egypt` |
| :western_sahara: | `western_sahara` | :eritrea: | `eritrea` |
| :es: | `es` | :ethiopia: | `ethiopia` |
| :eu: | `eu` <br /> `european_union` | :finland: | `finland` |
| :fiji: | `fiji` | :falkland_islands: | `falkland_islands` |
| :micronesia: | `micronesia` | :faroe_islands: | `faroe_islands` |
| :fr: | `fr` | :gabon: | `gabon` |
| :gb: | `gb` <br /> `uk` | :grenada: | `grenada` |
| :georgia: | `georgia` | :french_guiana: | `french_guiana` |
| :guernsey: | `guernsey` | :ghana: | `ghana` |
| :gibraltar: | `gibraltar` | :greenland: | `greenland` |
| :gambia: | `gambia` | :guinea: | `guinea` |
| :guadeloupe: | `guadeloupe` | :equatorial_guinea: | `equatorial_guinea` |
| :greece: | `greece` | :south_georgia_south_sandwich_islands: | `south_georgia_south_sandwich_islands` |
| :guatemala: | `guatemala` | :guam: | `guam` |
| :guinea_bissau: | `guinea_bissau` | :guyana: | `guyana` |
| :hong_kong: | `hong_kong` | :honduras: | `honduras` |
| :croatia: | `croatia` | :haiti: | `haiti` |
| :hungary: | `hungary` | :canary_islands: | `canary_islands` |
| :indonesia: | `indonesia` | :ireland: | `ireland` |
| :israel: | `israel` | :isle_of_man: | `isle_of_man` |
| :india: | `india` | :british_indian_ocean_territory: | `british_indian_ocean_territory` |
| :iraq: | `iraq` | :iran: | `iran` |
| :iceland: | `iceland` | :it: | `it` |
| :jersey: | `jersey` | :jamaica: | `jamaica` |
| :jordan: | `jordan` | :jp: | `jp` |
| :kenya: | `kenya` | :kyrgyzstan: | `kyrgyzstan` |
| :cambodia: | `cambodia` | :kiribati: | `kiribati` |
| :comoros: | `comoros` | :st_kitts_nevis: | `st_kitts_nevis` |
| :north_korea: | `north_korea` | :kr: | `kr` |
| :kuwait: | `kuwait` | :cayman_islands: | `cayman_islands` |
| :kazakhstan: | `kazakhstan` | :laos: | `laos` |
| :lebanon: | `lebanon` | :st_lucia: | `st_lucia` |
| :liechtenstein: | `liechtenstein` | :sri_lanka: | `sri_lanka` |
| :liberia: | `liberia` | :lesotho: | `lesotho` |
| :lithuania: | `lithuania` | :luxembourg: | `luxembourg` |
| :latvia: | `latvia` | :libya: | `libya` |
| :morocco: | `morocco` | :monaco: | `monaco` |
| :moldova: | `moldova` | :montenegro: | `montenegro` |
| :madagascar: | `madagascar` | :marshall_islands: | `marshall_islands` |
| :macedonia: | `macedonia` | :mali: | `mali` |
| :myanmar: | `myanmar` | :mongolia: | `mongolia` |
| :macau: | `macau` | :northern_mariana_islands: | `northern_mariana_islands` |
| :martinique: | `martinique` | :mauritania: | `mauritania` |
| :montserrat: | `montserrat` | :malta: | `malta` |
| :mauritius: | `mauritius` | :maldives: | `maldives` |
| :malawi: | `malawi` | :mexico: | `mexico` |
| :malaysia: | `malaysia` | :mozambique: | `mozambique` |
| :namibia: | `namibia` | :new_caledonia: | `new_caledonia` |
| :niger: | `niger` | :norfolk_island: | `norfolk_island` |
| :nigeria: | `nigeria` | :nicaragua: | `nicaragua` |
| :netherlands: | `netherlands` | :norway: | `norway` |
| :nepal: | `nepal` | :nauru: | `nauru` |
| :niue: | `niue` | :new_zealand: | `new_zealand` |
| :oman: | `oman` | :panama: | `panama` |
| :peru: | `peru` | :french_polynesia: | `french_polynesia` |
| :papua_new_guinea: | `papua_new_guinea` | :philippines: | `philippines` |
| :pakistan: | `pakistan` | :poland: | `poland` |
| :st_pierre_miquelon: | `st_pierre_miquelon` | :pitcairn_islands: | `pitcairn_islands` |
| :puerto_rico: | `puerto_rico` | :palestinian_territories: | `palestinian_territories` |
| :portugal: | `portugal` | :palau: | `palau` |
| :paraguay: | `paraguay` | :qatar: | `qatar` |
| :reunion: | `reunion` | :romania: | `romania` |
| :serbia: | `serbia` | :ru: | `ru` |
| :rwanda: | `rwanda` | :saudi_arabia: | `saudi_arabia` |
| :solomon_islands: | `solomon_islands` | :seychelles: | `seychelles` |
| :sudan: | `sudan` | :sweden: | `sweden` |
| :singapore: | `singapore` | :st_helena: | `st_helena` |
| :slovenia: | `slovenia` | :slovakia: | `slovakia` |
| :sierra_leone: | `sierra_leone` | :san_marino: | `san_marino` |
| :senegal: | `senegal` | :somalia: | `somalia` |
| :suriname: | `suriname` | :south_sudan: | `south_sudan` |
| :sao_tome_principe: | `sao_tome_principe` | :el_salvador: | `el_salvador` |
| :sint_maarten: | `sint_maarten` | :syria: | `syria` |
| :swaziland: | `swaziland` | :turks_caicos_islands: | `turks_caicos_islands` |
| :chad: | `chad` | :french_southern_territories: | `french_southern_territories` |
| :togo: | `togo` | :thailand: | `thailand` |
| :tajikistan: | `tajikistan` | :tokelau: | `tokelau` |
| :timor_leste: | `timor_leste` | :turkmenistan: | `turkmenistan` |
| :tunisia: | `tunisia` | :tonga: | `tonga` |
| :tr: | `tr` | :trinidad_tobago: | `trinidad_tobago` |
| :tuvalu: | `tuvalu` | :taiwan: | `taiwan` |
| :tanzania: | `tanzania` | :ukraine: | `ukraine` |
| :uganda: | `uganda` | :us: | `us` |
| :uruguay: | `uruguay` | :uzbekistan: | `uzbekistan` |
| :vatican_city: | `vatican_city` | :st_vincent_grenadines: | `st_vincent_grenadines` |
| :venezuela: | `venezuela` | :british_virgin_islands: | `british_virgin_islands` |
| :us_virgin_islands: | `us_virgin_islands` | :vietnam: | `vietnam` |
| :vanuatu: | `vanuatu` | :wallis_futuna: | `wallis_futuna` |
| :samoa: | `samoa` | :kosovo: | `kosovo` |
| :yemen: | `yemen` | :mayotte: | `mayotte` |
| :south_africa: | `south_africa` | :zambia: | `zambia` |
| :zimbabwe: | `zimbabwe` | | |


