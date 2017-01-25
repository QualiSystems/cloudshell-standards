



<!DOCTYPE html>
<html lang="en" class=" is-u2f-enabled">
  <head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb# object: http://ogp.me/ns/object# article: http://ogp.me/ns/article# profile: http://ogp.me/ns/profile#">
    <meta charset='utf-8'>
    

    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/frameworks-c07e6f4b02b556d1d85052fb3853caf84c80e6b23dcdb1ae1b00f051da1115a2.css" integrity="sha256-wH5vSwK1VtHYUFL7OFPK+EyA5rI9zbGuGwDwUdoRFaI=" media="all" rel="stylesheet" />
    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/github-85f6307e0a74c78ba00f8c5bf9c7fb17a418d361627638f51f989be45f709416.css" integrity="sha256-hfYwfgp0x4ugD4xb+cf7F6QY02Fidjj1H5ib5F9wlBY=" media="all" rel="stylesheet" />
    
    
    
    

    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="Content-Language" content="en">
    <meta name="viewport" content="width=device-width">
    
    <title>shell-firewall-standard/firewall_standard.md at master · QualiSystems/shell-firewall-standard</title>
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
    <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
    <link rel="apple-touch-icon" href="/apple-touch-icon.png">
    <link rel="apple-touch-icon" sizes="57x57" href="/apple-touch-icon-57x57.png">
    <link rel="apple-touch-icon" sizes="60x60" href="/apple-touch-icon-60x60.png">
    <link rel="apple-touch-icon" sizes="72x72" href="/apple-touch-icon-72x72.png">
    <link rel="apple-touch-icon" sizes="76x76" href="/apple-touch-icon-76x76.png">
    <link rel="apple-touch-icon" sizes="114x114" href="/apple-touch-icon-114x114.png">
    <link rel="apple-touch-icon" sizes="120x120" href="/apple-touch-icon-120x120.png">
    <link rel="apple-touch-icon" sizes="144x144" href="/apple-touch-icon-144x144.png">
    <link rel="apple-touch-icon" sizes="152x152" href="/apple-touch-icon-152x152.png">
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon-180x180.png">
    <meta property="fb:app_id" content="1401488693436528">

      <meta content="https://avatars2.githubusercontent.com/u/15384617?v=3&amp;s=400" name="twitter:image:src" /><meta content="@github" name="twitter:site" /><meta content="summary" name="twitter:card" /><meta content="QualiSystems/shell-firewall-standard" name="twitter:title" /><meta content="shell-firewall-standard - CloudShell Shell standard definition for Firewall type devices/virtual appliances" name="twitter:description" />
      <meta content="https://avatars2.githubusercontent.com/u/15384617?v=3&amp;s=400" property="og:image" /><meta content="GitHub" property="og:site_name" /><meta content="object" property="og:type" /><meta content="QualiSystems/shell-firewall-standard" property="og:title" /><meta content="https://github.com/QualiSystems/shell-firewall-standard" property="og:url" /><meta content="shell-firewall-standard - CloudShell Shell standard definition for Firewall type devices/virtual appliances" property="og:description" />
      <meta name="browser-stats-url" content="https://api.github.com/_private/browser/stats">
    <meta name="browser-errors-url" content="https://api.github.com/_private/browser/errors">
    <link rel="assets" href="https://assets-cdn.github.com/">
    <link rel="web-socket" href="wss://live.github.com/_sockets/VjI6MTA4OTIwNTExOjM1YmRjZTYyMTcwNjg5MTBiYjczMjA0NDUzZGEzMWU2ZjJmZWY5MDM4MzA5OWZiYzM5MWYzYTExN2I3NWM0Zjg=--8c1522899c9a9b7900b0db6c05cd4f4a2746a737">
    <meta name="pjax-timeout" content="1000">
    <link rel="sudo-modal" href="/sessions/sudo_modal">
    <meta name="request-id" content="D6A1:200C:417F501:6AC82A4:58887154" data-pjax-transient>

    <meta name="msapplication-TileImage" content="/windows-tile.png">
    <meta name="msapplication-TileColor" content="#ffffff">
    <meta name="selected-link" value="repo_source" data-pjax-transient>

    <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
<meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-analytics" content="UA-3769691-2">

<meta content="collector.githubapp.com" name="octolytics-host" /><meta content="github" name="octolytics-app-id" /><meta content="D6A1:200C:417F501:6AC82A4:58887154" name="octolytics-dimension-request_id" /><meta content="17066349" name="octolytics-actor-id" /><meta content="menib" name="octolytics-actor-login" /><meta content="71754e03923c5fd1ad15d35df0ab8918f12ae72b64d203ed00386c9d7fc88f5a" name="octolytics-actor-hash" />
<meta content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" name="analytics-location" />



  <meta class="js-ga-set" name="dimension1" content="Logged In">



        <meta name="hostname" content="github.com">
    <meta name="user-login" content="menib">

        <meta name="expected-hostname" content="github.com">
      <meta name="js-proxy-site-detection-payload" content="MzdhZjk1MzFhMDJjM2I0ZGFiYzg5Mjc2ZjY1M2NhYTg2NmQ2NzdhOWJhMGEyMTE2MWEwZDBhMzIxMDcxY2QyMnx7InJlbW90ZV9hZGRyZXNzIjoiODIuODAuMzUuMjI2IiwicmVxdWVzdF9pZCI6IkQ2QTE6MjAwQzo0MTdGNTAxOjZBQzgyQTQ6NTg4ODcxNTQiLCJ0aW1lc3RhbXAiOjE0ODUzMzY5MTksImhvc3QiOiJnaXRodWIuY29tIn0=">


      <link rel="mask-icon" href="https://assets-cdn.github.com/pinned-octocat.svg" color="#000000">
      <link rel="icon" type="image/x-icon" href="https://assets-cdn.github.com/favicon.ico">

    <meta name="html-safe-nonce" content="b775c8f1608af02c89d229e927b365c438c01468">

    <meta http-equiv="x-pjax-version" content="a0d44715f0023df63908ae97906689f8">
    

      
  <meta name="description" content="shell-firewall-standard - CloudShell Shell standard definition for Firewall type devices/virtual appliances">
  <meta name="go-import" content="github.com/QualiSystems/shell-firewall-standard git https://github.com/QualiSystems/shell-firewall-standard.git">

  <meta content="15384617" name="octolytics-dimension-user_id" /><meta content="QualiSystems" name="octolytics-dimension-user_login" /><meta content="63520461" name="octolytics-dimension-repository_id" /><meta content="QualiSystems/shell-firewall-standard" name="octolytics-dimension-repository_nwo" /><meta content="true" name="octolytics-dimension-repository_public" /><meta content="false" name="octolytics-dimension-repository_is_fork" /><meta content="63520461" name="octolytics-dimension-repository_network_root_id" /><meta content="QualiSystems/shell-firewall-standard" name="octolytics-dimension-repository_network_root_nwo" />
  <link href="https://github.com/QualiSystems/shell-firewall-standard/commits/master.atom" rel="alternate" title="Recent Commits to shell-firewall-standard:master" type="application/atom+xml">


      <link rel="canonical" href="https://github.com/QualiSystems/shell-firewall-standard/blob/master/spec/firewall_standard.md" data-pjax-transient>
  </head>


  <body class="logged-in  env-production windows vis-public page-blob">
    <div id="js-pjax-loader-bar" class="pjax-loader-bar"><div class="progress"></div></div>
    <a href="#start-of-content" tabindex="1" class="accessibility-aid js-skip-to-content">Skip to content</a>

    
    
    



        <div class="header header-logged-in true" role="banner">
  <div class="container clearfix">

    <a class="header-logo-invertocat" href="https://github.com/" data-hotkey="g d" aria-label="Homepage" data-ga-click="Header, go to dashboard, icon:logo">
  <svg aria-hidden="true" class="octicon octicon-mark-github" height="28" version="1.1" viewBox="0 0 16 16" width="28"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>


        <div class="header-search scoped-search site-scoped-search js-site-search" role="search">
  <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/QualiSystems/shell-firewall-standard/search" class="js-site-search-form" data-scoped-search-url="/QualiSystems/shell-firewall-standard/search" data-unscoped-search-url="/search" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <label class="form-control header-search-wrapper js-chromeless-input-container">
      <div class="header-search-scope">This repository</div>
      <input type="text"
        class="form-control header-search-input js-site-search-focus js-site-search-field is-clearable"
        data-hotkey="s"
        name="q"
        placeholder="Search"
        aria-label="Search this repository"
        data-unscoped-placeholder="Search GitHub"
        data-scoped-placeholder="Search"
        autocapitalize="off">
    </label>
</form></div>


      <ul class="header-nav float-left" role="navigation">
        <li class="header-nav-item">
          <a href="/pulls" aria-label="Pull requests you created" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:pulls context:user" data-hotkey="g p" data-selected-links="/pulls /pulls/assigned /pulls/mentioned /pulls">
            Pull requests
</a>        </li>
        <li class="header-nav-item">
          <a href="/issues" aria-label="Issues you created" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:issues context:user" data-hotkey="g i" data-selected-links="/issues /issues/assigned /issues/mentioned /issues">
            Issues
</a>        </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="https://gist.github.com/" data-ga-click="Header, go to gist, text:gist">Gist</a>
          </li>
      </ul>

    
<ul class="header-nav user-nav float-right" id="user-links">
  <li class="header-nav-item">
    

  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link tooltipped tooltipped-s js-menu-target" href="/new"
       aria-label="Create new…"
       data-ga-click="Header, create new, icon:add">
      <svg aria-hidden="true" class="octicon octicon-plus float-left" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 9H7v5H5V9H0V7h5V2h2v5h5z"/></svg>
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <ul class="dropdown-menu dropdown-menu-sw">
        
<a class="dropdown-item" href="/new" data-ga-click="Header, create new repository">
  New repository
</a>

  <a class="dropdown-item" href="/new/import" data-ga-click="Header, import a repository">
    Import repository
  </a>

<a class="dropdown-item" href="https://gist.github.com/" data-ga-click="Header, create new gist">
  New gist
</a>

  <a class="dropdown-item" href="/organizations/new" data-ga-click="Header, create new organization">
    New organization
  </a>



  <div class="dropdown-divider"></div>
  <div class="dropdown-header">
    <span title="QualiSystems/shell-firewall-standard">This repository</span>
  </div>
    <a class="dropdown-item" href="/QualiSystems/shell-firewall-standard/issues/new" data-ga-click="Header, create new issue">
      New issue
    </a>

      </ul>
    </div>
  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link name tooltipped tooltipped-sw js-menu-target" href="/menib"
       aria-label="View profile and more"
       data-ga-click="Header, show menu, icon:avatar">
      <img alt="@menib" class="avatar" height="20" src="https://avatars3.githubusercontent.com/u/17066349?v=3&amp;s=40" width="20" />
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <div class="dropdown-menu dropdown-menu-sw">
        <div class="dropdown-header header-nav-current-user css-truncate">
          Signed in as <strong class="css-truncate-target">menib</strong>
        </div>

        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/menib" data-ga-click="Header, go to profile, text:your profile">
          Your profile
        </a>
        <a class="dropdown-item" href="/menib?tab=stars" data-ga-click="Header, go to starred repos, text:your stars">
          Your stars
        </a>
        <a class="dropdown-item" href="/explore" data-ga-click="Header, go to explore, text:explore">
          Explore
        </a>
          <a class="dropdown-item" href="/integrations" data-ga-click="Header, go to integrations, text:integrations">
            Integrations
          </a>
        <a class="dropdown-item" href="https://help.github.com" data-ga-click="Header, go to help, text:help">
          Help
        </a>

        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/settings/profile" data-ga-click="Header, go to settings, icon:settings">
          Settings
        </a>

        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/logout" class="logout-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="JD7lOks89/LlwL+N3Kh+z5oZldSyX2rba89UYBaIL7Gv05cGxcgXUphNb0bbsr1cfwkNLGGeNcH2vEBmaYJ1vA==" /></div>
          <button type="submit" class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
            Sign out
          </button>
</form>      </div>
    </div>
  </li>
</ul>


    
  </div>
</div>


      


    <div id="start-of-content" class="accessibility-aid"></div>

      <div id="js-flash-container">
</div>


    <div role="main">
        <div itemscope itemtype="http://schema.org/SoftwareSourceCode">
    <div id="js-repo-pjax-container" data-pjax-container>
      
<div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav">
  <div class="container repohead-details-container">

    

<ul class="pagehead-actions">

  <li>
        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/notifications/subscribe" class="js-social-container" data-autosubmit="true" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="r9vjHlQ7lNl1rOcn8Ftv8gDacmY/YwH4LCDX5mrGWbBue7lTc6frFztJqxz5zgSjbgpgMuHwOWhaGHrdFdXXXg==" /></div>      <input class="form-control" id="repository_id" name="repository_id" type="hidden" value="63520461" />

        <div class="select-menu js-menu-container js-select-menu">
          <a href="/QualiSystems/shell-firewall-standard/subscription"
            class="btn btn-sm btn-with-count select-menu-button js-menu-target" role="button" tabindex="0" aria-haspopup="true"
            data-ga-click="Repository, click Watch settings, action:blob#show">
            <span class="js-select-button">
              <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
              Unwatch
            </span>
          </a>
          <a class="social-count js-social-count"
            href="/QualiSystems/shell-firewall-standard/watchers"
            aria-label="7 users are watching this repository">
            7
          </a>

        <div class="select-menu-modal-holder">
          <div class="select-menu-modal subscription-menu-modal js-menu-content" aria-hidden="true">
            <div class="select-menu-header js-navigation-enable" tabindex="-1">
              <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
              <span class="select-menu-title">Notifications</span>
            </div>

              <div class="select-menu-list js-navigation-container" role="menu">

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input id="do_included" name="do" type="radio" value="included" />
                    <span class="select-menu-item-heading">Not watching</span>
                    <span class="description">Be notified when participating or @mentioned.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                      Watch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item selected" role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input checked="checked" id="do_subscribed" name="do" type="radio" value="subscribed" />
                    <span class="select-menu-item-heading">Watching</span>
                    <span class="description">Be notified of all conversations.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                      Unwatch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input id="do_ignore" name="do" type="radio" value="ignore" />
                    <span class="select-menu-item-heading">Ignoring</span>
                    <span class="description">Never be notified.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-mute" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8 2.81v10.38c0 .67-.81 1-1.28.53L3 10H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h2l3.72-3.72C7.19 1.81 8 2.14 8 2.81zm7.53 3.22l-1.06-1.06-1.97 1.97-1.97-1.97-1.06 1.06L11.44 8 9.47 9.97l1.06 1.06 1.97-1.97 1.97 1.97 1.06-1.06L13.56 8l1.97-1.97z"/></svg>
                      Stop ignoring
                    </span>
                  </div>
                </div>

              </div>

            </div>
          </div>
        </div>
</form>
  </li>

  <li>
      <div class="js-toggler-container js-social-container starring-container ">
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/QualiSystems/shell-firewall-standard/unstar" class="starred" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="fBdy4YeMpltabO5aC/BwgBVtH2aD7L1S3OFmu4+QW5hJ7Qr9UwDGd1nOzdUvHk+B/gzJAdf6fnzyE9nisDH1IA==" /></div>
      <button
        type="submit"
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Unstar this repository" title="Unstar QualiSystems/shell-firewall-standard"
        data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"/></svg>
        Unstar
      </button>
        <a class="social-count js-social-count" href="/QualiSystems/shell-firewall-standard/stargazers"
           aria-label="0 users starred this repository">
          0
        </a>
</form>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/QualiSystems/shell-firewall-standard/star" class="unstarred" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="33aVdPkHtobH99EANCdVwR1UHqS1uvtG48yxl3kCt5hcMvH0O9napwgQKCDzhck4iK6BKX8w8BUzk7JQyBJ2Bw==" /></div>
      <button
        type="submit"
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Star this repository" title="Star QualiSystems/shell-firewall-standard"
        data-ga-click="Repository, click star button, action:blob#show; text:Star">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"/></svg>
        Star
      </button>
        <a class="social-count js-social-count" href="/QualiSystems/shell-firewall-standard/stargazers"
           aria-label="0 users starred this repository">
          0
        </a>
</form>  </div>

  </li>

  <li>
          <a href="#fork-destination-box" class="btn btn-sm btn-with-count"
              title="Fork your own copy of QualiSystems/shell-firewall-standard to your account"
              aria-label="Fork your own copy of QualiSystems/shell-firewall-standard to your account"
              rel="facebox"
              data-ga-click="Repository, show fork modal, action:blob#show; text:Fork">
              <svg aria-hidden="true" class="octicon octicon-repo-forked" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path fill-rule="evenodd" d="M8 1a1.993 1.993 0 0 0-1 3.72V6L5 8 3 6V4.72A1.993 1.993 0 0 0 2 1a1.993 1.993 0 0 0-1 3.72V6.5l3 3v1.78A1.993 1.993 0 0 0 5 15a1.993 1.993 0 0 0 1-3.72V9.5l3-3V4.72A1.993 1.993 0 0 0 8 1zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3 10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3-10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
            Fork
          </a>

          <div id="fork-destination-box" style="display: none;">
            <h2 class="facebox-header" data-facebox-id="facebox-header">Where should we fork this repository?</h2>
            <include-fragment src=""
                class="js-fork-select-fragment fork-select-fragment"
                data-url="/QualiSystems/shell-firewall-standard/fork?fragment=1">
              <img alt="Loading" height="64" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-128.gif" width="64" />
            </include-fragment>
          </div>

    <a href="/QualiSystems/shell-firewall-standard/network" class="social-count"
       aria-label="2 users forked this repository">
      2
    </a>
  </li>
</ul>

    <h1 class="public ">
  <svg aria-hidden="true" class="octicon octicon-repo" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M4 9H3V8h1v1zm0-3H3v1h1V6zm0-2H3v1h1V4zm0-2H3v1h1V2zm8-1v12c0 .55-.45 1-1 1H6v2l-1.5-1.5L3 16v-2H1c-.55 0-1-.45-1-1V1c0-.55.45-1 1-1h10c.55 0 1 .45 1 1zm-1 10H1v2h2v-1h3v1h5v-2zm0-10H2v9h9V1z"/></svg>
  <span class="author" itemprop="author"><a href="/QualiSystems" class="url fn" rel="author">QualiSystems</a></span><!--
--><span class="path-divider">/</span><!--
--><strong itemprop="name"><a href="/QualiSystems/shell-firewall-standard" data-pjax="#js-repo-pjax-container">shell-firewall-standard</a></strong>

</h1>

  </div>
  <div class="container">
    
<nav class="reponav js-repo-nav js-sidenav-container-pjax"
     itemscope
     itemtype="http://schema.org/BreadcrumbList"
     role="navigation"
     data-pjax="#js-repo-pjax-container">

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/QualiSystems/shell-firewall-standard" class="js-selected-navigation-item selected reponav-item" data-hotkey="g c" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches /QualiSystems/shell-firewall-standard" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-code" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M9.5 3L8 4.5 11.5 8 8 11.5 9.5 13 14 8 9.5 3zm-5 0L0 8l4.5 5L6 11.5 2.5 8 6 4.5 4.5 3z"/></svg>
      <span itemprop="name">Code</span>
      <meta itemprop="position" content="1">
</a>  </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a href="/QualiSystems/shell-firewall-standard/issues" class="js-selected-navigation-item reponav-item" data-hotkey="g i" data-selected-links="repo_issues repo_labels repo_milestones /QualiSystems/shell-firewall-standard/issues" itemprop="url">
        <svg aria-hidden="true" class="octicon octicon-issue-opened" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7s-2.56 5.7-5.7 5.7A5.71 5.71 0 0 1 1.3 8c0-3.14 2.56-5.7 5.7-5.7zM7 1C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7-3.14-7-7-7zm1 3H6v5h2V4zm0 6H6v2h2v-2z"/></svg>
        <span itemprop="name">Issues</span>
        <span class="counter">0</span>
        <meta itemprop="position" content="2">
</a>    </span>

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/QualiSystems/shell-firewall-standard/pulls" class="js-selected-navigation-item reponav-item" data-hotkey="g p" data-selected-links="repo_pulls /QualiSystems/shell-firewall-standard/pulls" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-git-pull-request" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M11 11.28V5c-.03-.78-.34-1.47-.94-2.06C9.46 2.35 8.78 2.03 8 2H7V0L4 3l3 3V4h1c.27.02.48.11.69.31.21.2.3.42.31.69v6.28A1.993 1.993 0 0 0 10 15a1.993 1.993 0 0 0 1-3.72zm-1 2.92c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zM4 3c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v6.56A1.993 1.993 0 0 0 2 15a1.993 1.993 0 0 0 1-3.72V4.72c.59-.34 1-.98 1-1.72zm-.8 10c0 .66-.55 1.2-1.2 1.2-.65 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
      <span itemprop="name">Pull requests</span>
      <span class="counter">0</span>
      <meta itemprop="position" content="3">
</a>  </span>

  <a href="/QualiSystems/shell-firewall-standard/projects" class="js-selected-navigation-item reponav-item" data-selected-links="repo_projects new_repo_project repo_project /QualiSystems/shell-firewall-standard/projects">
    <svg aria-hidden="true" class="octicon octicon-project" height="16" version="1.1" viewBox="0 0 15 16" width="15"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
    Projects
    <span class="counter">0</span>
</a>
    <a href="/QualiSystems/shell-firewall-standard/wiki" class="js-selected-navigation-item reponav-item" data-hotkey="g w" data-selected-links="repo_wiki /QualiSystems/shell-firewall-standard/wiki">
      <svg aria-hidden="true" class="octicon octicon-book" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M3 5h4v1H3V5zm0 3h4V7H3v1zm0 2h4V9H3v1zm11-5h-4v1h4V5zm0 2h-4v1h4V7zm0 2h-4v1h4V9zm2-6v9c0 .55-.45 1-1 1H9.5l-1 1-1-1H2c-.55 0-1-.45-1-1V3c0-.55.45-1 1-1h5.5l1 1 1-1H15c.55 0 1 .45 1 1zm-8 .5L7.5 3H2v9h6V3.5zm7-.5H9.5l-.5.5V12h6V3z"/></svg>
      Wiki
</a>

  <a href="/QualiSystems/shell-firewall-standard/pulse" class="js-selected-navigation-item reponav-item" data-selected-links="pulse /QualiSystems/shell-firewall-standard/pulse">
    <svg aria-hidden="true" class="octicon octicon-pulse" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M11.5 8L8.8 5.4 6.6 8.5 5.5 1.6 2.38 8H0v2h3.6l.9-1.8.9 5.4L9 8.5l1.6 1.5H14V8z"/></svg>
    Pulse
</a>
  <a href="/QualiSystems/shell-firewall-standard/graphs" class="js-selected-navigation-item reponav-item" data-selected-links="repo_graphs repo_contributors /QualiSystems/shell-firewall-standard/graphs">
    <svg aria-hidden="true" class="octicon octicon-graph" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M16 14v1H0V0h1v14h15zM5 13H3V8h2v5zm4 0H7V3h2v10zm4 0h-2V6h2v7z"/></svg>
    Graphs
</a>

</nav>

  </div>
</div>

<div class="container new-discussion-timeline experiment-repo-nav">
  <div class="repository-content">

    

<a href="/QualiSystems/shell-firewall-standard/blob/ed0e7b9bd80bb38624c88b4702efb820bab75364/spec/firewall_standard.md" class="d-none js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:00b612da0eb357e03549a211fdf89cb5 -->

<div class="file-navigation js-zeroclipboard-container">
  
<div class="select-menu branch-select-menu js-menu-container js-select-menu float-left">
  <button class="btn btn-sm select-menu-button js-menu-target css-truncate" data-hotkey="w"
    
    type="button" aria-label="Switch branches or tags" tabindex="0" aria-haspopup="true">
    <i>Branch:</i>
    <span class="js-select-button css-truncate-target">master</span>
  </button>

  <div class="select-menu-modal-holder js-menu-content js-navigation-container" data-pjax aria-hidden="true">

    <div class="select-menu-modal">
      <div class="select-menu-header">
        <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
        <span class="select-menu-title">Switch branches/tags</span>
      </div>

      <div class="select-menu-filters">
        <div class="select-menu-text-filter">
          <input type="text" aria-label="Find or create a branch…" id="context-commitish-filter-field" class="form-control js-filterable-field js-navigation-enable" placeholder="Find or create a branch…">
        </div>
        <div class="select-menu-tabs">
          <ul>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="branches" data-filter-placeholder="Find or create a branch…" class="js-select-menu-tab" role="tab">Branches</a>
            </li>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="tags" data-filter-placeholder="Find a tag…" class="js-select-menu-tab" role="tab">Tags</a>
            </li>
          </ul>
        </div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="branches" role="menu">

        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/QualiSystems/shell-firewall-standard/blob/feature_move2standard2.0/spec/firewall_standard.md"
               data-name="feature_move2standard2.0"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                feature_move2standard2.0
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/QualiSystems/shell-firewall-standard/blob/master/spec/firewall_standard.md"
               data-name="master"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                master
              </span>
            </a>
        </div>

          <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/QualiSystems/shell-firewall-standard/branches" class="js-create-branch select-menu-item select-menu-new-item-form js-navigation-item js-new-item-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="DTCaiPvoiElwLcRxTFAdfsdGBRBNuDcL5uA4yl7XceHL70ErwcbtMXHQO7k6xkc3Fzx2fAwpcIV+BxXxL1oXJw==" /></div>
          <svg aria-hidden="true" class="octicon octicon-git-branch select-menu-item-icon" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path fill-rule="evenodd" d="M10 5c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v.3c-.02.52-.23.98-.63 1.38-.4.4-.86.61-1.38.63-.83.02-1.48.16-2 .45V4.72a1.993 1.993 0 0 0-1-3.72C.88 1 0 1.89 0 3a2 2 0 0 0 1 1.72v6.56c-.59.35-1 .99-1 1.72 0 1.11.89 2 2 2 1.11 0 2-.89 2-2 0-.53-.2-1-.53-1.36.09-.06.48-.41.59-.47.25-.11.56-.17.94-.17 1.05-.05 1.95-.45 2.75-1.25S8.95 7.77 9 6.73h-.02C9.59 6.37 10 5.73 10 5zM2 1.8c.66 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2C1.35 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2zm0 12.41c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm6-8c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
            <div class="select-menu-item-text">
              <span class="select-menu-item-heading">Create branch: <span class="js-new-item-name"></span></span>
              <span class="description">from ‘master’</span>
            </div>
            <input type="hidden" name="name" id="name" class="js-new-item-value">
            <input type="hidden" name="branch" id="branch" value="master">
            <input type="hidden" name="path" id="path" value="spec/firewall_standard.md">
</form>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="tags">
        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


        </div>

        <div class="select-menu-no-results">Nothing to show</div>
      </div>

    </div>
  </div>
</div>

  <div class="BtnGroup float-right">
    <a href="/QualiSystems/shell-firewall-standard/find/master"
          class="js-pjax-capture-input btn btn-sm BtnGroup-item"
          data-pjax
          data-hotkey="t">
      Find file
    </a>
    <button aria-label="Copy file path to clipboard" class="js-zeroclipboard btn btn-sm BtnGroup-item tooltipped tooltipped-s" data-copied-hint="Copied!" type="button">Copy path</button>
  </div>
  <div class="breadcrumb js-zeroclipboard-target">
    <span class="repo-root js-repo-root"><span class="js-path-segment"><a href="/QualiSystems/shell-firewall-standard"><span>shell-firewall-standard</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a href="/QualiSystems/shell-firewall-standard/tree/master/spec"><span>spec</span></a></span><span class="separator">/</span><strong class="final-path">firewall_standard.md</strong>
  </div>
</div>


  <div class="commit-tease">
      <span class="float-right">
        <a class="commit-tease-sha" href="/QualiSystems/shell-firewall-standard/commit/ed0e7b9bd80bb38624c88b4702efb820bab75364" data-pjax>
          ed0e7b9
        </a>
        <relative-time datetime="2017-01-23T14:48:05Z">Jan 23, 2017</relative-time>
      </span>
      <div>
        <img alt="@GalcQuali" class="avatar" height="20" src="https://avatars2.githubusercontent.com/u/16877134?v=3&amp;s=40" width="20" />
        <a href="/GalcQuali" class="user-mention" rel="contributor">GalcQuali</a>
          <a href="/QualiSystems/shell-firewall-standard/commit/ed0e7b9bd80bb38624c88b4702efb820bab75364" class="message" data-pjax="true" title="Typo fix">Typo fix</a>
      </div>

    <div class="commit-tease-contributors">
      <button type="button" class="btn-link muted-link contributors-toggle" data-facebox="#blob_contributors_box">
        <strong>4</strong>
         contributors
      </button>
          <a class="avatar-link tooltipped tooltipped-s" aria-label="menib" href="/QualiSystems/shell-firewall-standard/commits/master/spec/firewall_standard.md?author=menib"><img alt="@menib" class="avatar" height="20" src="https://avatars3.githubusercontent.com/u/17066349?v=3&amp;s=40" width="20" /> </a>
    <a class="avatar-link tooltipped tooltipped-s" aria-label="GalcQuali" href="/QualiSystems/shell-firewall-standard/commits/master/spec/firewall_standard.md?author=GalcQuali"><img alt="@GalcQuali" class="avatar" height="20" src="https://avatars2.githubusercontent.com/u/16877134?v=3&amp;s=40" width="20" /> </a>
    <a class="avatar-link tooltipped tooltipped-s" aria-label="alonagetzler" href="/QualiSystems/shell-firewall-standard/commits/master/spec/firewall_standard.md?author=alonagetzler"><img alt="@alonagetzler" class="avatar" height="20" src="https://avatars1.githubusercontent.com/u/16175869?v=3&amp;s=40" width="20" /> </a>
    <a class="avatar-link tooltipped tooltipped-s" aria-label="doppleware" href="/QualiSystems/shell-firewall-standard/commits/master/spec/firewall_standard.md?author=doppleware"><img alt="@doppleware" class="avatar" height="20" src="https://avatars2.githubusercontent.com/u/93863?v=3&amp;s=40" width="20" /> </a>


    </div>

    <div id="blob_contributors_box" style="display:none">
      <h2 class="facebox-header" data-facebox-id="facebox-header">Users who have contributed to this file</h2>
      <ul class="facebox-user-list" data-facebox-id="facebox-description">
          <li class="facebox-user-list-item">
            <img alt="@menib" height="24" src="https://avatars1.githubusercontent.com/u/17066349?v=3&amp;s=48" width="24" />
            <a href="/menib">menib</a>
          </li>
          <li class="facebox-user-list-item">
            <img alt="@GalcQuali" height="24" src="https://avatars0.githubusercontent.com/u/16877134?v=3&amp;s=48" width="24" />
            <a href="/GalcQuali">GalcQuali</a>
          </li>
          <li class="facebox-user-list-item">
            <img alt="@alonagetzler" height="24" src="https://avatars3.githubusercontent.com/u/16175869?v=3&amp;s=48" width="24" />
            <a href="/alonagetzler">alonagetzler</a>
          </li>
          <li class="facebox-user-list-item">
            <img alt="@doppleware" height="24" src="https://avatars0.githubusercontent.com/u/93863?v=3&amp;s=48" width="24" />
            <a href="/doppleware">doppleware</a>
          </li>
      </ul>
    </div>
  </div>


<div class="file">
  <div class="file-header">
  <div class="file-actions">

    <div class="BtnGroup">
      <a href="/QualiSystems/shell-firewall-standard/raw/master/spec/firewall_standard.md" class="btn btn-sm BtnGroup-item" id="raw-url">Raw</a>
        <a href="/QualiSystems/shell-firewall-standard/blame/master/spec/firewall_standard.md" class="btn btn-sm js-update-url-with-hash BtnGroup-item" data-hotkey="b">Blame</a>
      <a href="/QualiSystems/shell-firewall-standard/commits/master/spec/firewall_standard.md" class="btn btn-sm BtnGroup-item" rel="nofollow">History</a>
    </div>

        <a class="btn-octicon tooltipped tooltipped-nw"
           href="github-windows://openRepo/https://github.com/QualiSystems/shell-firewall-standard?branch=master&amp;filepath=spec%2Ffirewall_standard.md"
           aria-label="Open this file in GitHub Desktop"
           data-ga-click="Repository, open with desktop, type:windows">
            <svg aria-hidden="true" class="octicon octicon-device-desktop" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"/></svg>
        </a>

        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/QualiSystems/shell-firewall-standard/edit/master/spec/firewall_standard.md" class="inline-form js-update-url-with-hash" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="Ic0WeL+nsdvAJEGOaAgwmls2d5SCh5muNimtI+qs1S/UMnjTQ//rmmP4eINnpfHJ3DhZLQaLxVVGJUdWS03aAw==" /></div>
          <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
            aria-label="Edit this file" data-hotkey="e" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-pencil" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"/></svg>
          </button>
</form>        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/QualiSystems/shell-firewall-standard/delete/master/spec/firewall_standard.md" class="inline-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="XY/2tyDS9qyJCEYGfJsEftBwyFz2PuosZ/vlZ+4W508kWYhnAsxGtDTvH2o/um2hJKtC20BAZFl0iDNstTxL7A==" /></div>
          <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
            aria-label="Delete this file" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-trashcan" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M11 2H9c0-.55-.45-1-1-1H5c-.55 0-1 .45-1 1H2c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1v9c0 .55.45 1 1 1h7c.55 0 1-.45 1-1V5c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm-1 12H3V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9zm1-10H2V3h9v1z"/></svg>
          </button>
</form>  </div>

  <div class="file-info">
      471 lines (362 sloc)
      <span class="file-info-divider"></span>
    25.8 KB
  </div>
</div>

  
  <div id="readme" class="readme blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="text"><h1><a id="user-content-firewall-shell-standard" class="anchor" href="#firewall-shell-standard" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Firewall Shell Standard</h1>

<h4><a id="user-content-version-300" class="anchor" href="#version-300" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Version 3.0.0</h4>

<h2><a id="user-content-introduction" class="anchor" href="#introduction" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Introduction</h2>

<p>The Firewall Shell Standard is a project used to define a standard for all Firewall Shells that integrate with CloudShell. The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in Firewall Shells development and customization.</p>

<h2><a id="user-content-revision-history" class="anchor" href="#revision-history" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Revision History</h2>

<table><thead>
<tr>
<th>Version</th>
<th>Date</th>
<th>Notes</th>
</tr>
</thead><tbody>
<tr>
<td>3.0.0</td>
<td>2017-01-23</td>
<td>1) Added letters to resources address. 2) Changed the type of the following attributes to "Password": "SNMP Read Community", "SNMP Write Community" and "SNMP V3 Password". Those changes are NOT backwards compatible.</td>
</tr>
<tr>
<td>2.0.0</td>
<td>2016-08-16</td>
<td>1) Added a new attribute named “CLI TCP Port” on the root model. That attribute will be filled in by the administrator (optional). 2)  The "Configuration Type" input in the Save and Restore command is now not mandatory, the default value if kept empty is Running. 3) Descriptions were added to the attributes, commands and command inputs (only commands visible in the UI). 4) A “Health check” command was added. This command performs checks on the device that validates that the Shell can work. In a firewall device this checks usually include connectivity check for the protocols used by the Shell. 5) Removed the attribute “Protocol Type” from the standard. 6) Added the attributes “Enable SNMP” and “Disable SNMP” on the root model. Those attribute will allow automatic configuration of SNMP before and after the execution of the Autoload command which requires SNMP. 7) The value of the attribute “Bandwidth” is now in MB instead of Bytes. 8) Added orchestration_save and orchestration_restore commands according to the Save and Restore Orchestration Standard. Those commands wrap the Shell’s Save and Restore commands with a standard interface to be used by the Sandbox orchestration. 9) The command name and command input names are now defined in the standard. Prior to this standard version only the command alias and command input aliases were defined. 10) The inputs of the load_firmware command were changed and alligned with the inputs of the restore command. 11) The expected syntax of the path and folder_path inputs of the restore, load_firmware and save commands in case of FTP protocol was clarified. <strong>The 9th and 10th items aren't backwards compatible and will require modification of any existing automation which calls the Shell’s commands. However, upcoming shells will still have the old commands available as hidden command so the shells themselves will remain backwards compatible until their next major verion.</strong></td>
</tr>
<tr>
<td>1.0.0</td>
<td>2016-06-23</td>
<td>First release of the Firewall Shell Standard</td>
</tr>
</tbody></table>

<h2><a id="user-content-definitions" class="anchor" href="#definitions" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Definitions</h2>

<h3><a id="user-content-granularity" class="anchor" href="#granularity" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Granularity</h3>

<p>A Firewall Shell should support all Firewall devices with the same Vendor and OS. For example a correct shell granularity will be “Cisco ASA Shell” and not “Cisco ASA 5500 Shell”.</p>

<h3><a id="user-content-specific-models-certification" class="anchor" href="#specific-models-certification" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Specific Models Certification</h3>

<p>Each released Shell should have a list of certified models. Model certification can be done only by Quali’s engineering, and validates that all the Shell’s capabilities are working for a specific model.
The Shell should also work for non-certified models, and in case some gaps are found a new version of the Shell will be released with the gaps addressed and the model certified.</p>

<h3><a id="user-content-generic-data-model" class="anchor" href="#generic-data-model" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Data Model</h3>

<p>All Firewall Shells share the same generic data model, except the model of the root level which is different per each Shell. The data model shouldn’t be modified.
The attributes associated with those generic models are also shared by all firewall Shells and their values are populated by the driver. It is allowed to add custom attributes only to the root level model, and it isn’t allowed to remove attributes from any level.</p>

<h3><a id="user-content-versioning" class="anchor" href="#versioning" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Versioning</h3>

<p>The Firewall Shell version follows Semantic Versioning Guidelines (see details in <a href="http://semver.org">http://semver.org</a>). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.</p>

<h3><a id="user-content-dependencies" class="anchor" href="#dependencies" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Dependencies</h3>

<p>In case the Firewall shell is written in Python and has dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions, for example to “cloudshell-firewall-cisco-asa 2.1.X”.
The dependency to cloudshell-automation-api will be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).</p>

<h2><a id="user-content-data-model" class="anchor" href="#data-model" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Data Model</h2>

<h3><a id="user-content-families--models" class="anchor" href="#families--models" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Families &amp; Models</h3>

<p>The firewall shell standard supports Firewall devices.</p>

<h4><a id="user-content-firewall-data-model" class="anchor" href="#firewall-data-model" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Firewall Data Model</h4>

<ul>
<li>Firewall

<ul>
<li>Chassis

<ul>
<li>Module

<ul>
<li>Port</li>
<li>Sub Module

<ul>
<li>Port</li>
</ul></li>
</ul></li>
<li>Port</li>
<li>Power Port</li>
</ul></li>
<li>Port Channel</li>
</ul></li>
</ul>

<h5><a id="user-content-example" class="anchor" href="#example" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Example:</h5>

<ul>
<li>Family: Firewall, Model: Cisco ASA Firewall

<ul>
<li>Family: Chassis, Model: Generic Chassis

<ul>
<li>Family: Module, Model: Generic Module

<ul>
<li>Family: Port, Model: Generic Port</li>
<li>Family: Sub Module, Model: Generic Sub Module

<ul>
<li>Family: Port, Model: Generic Port</li>
</ul></li>
</ul></li>
<li>Family: Port, Model: Generic Port</li>
<li>Family: Power Port, Model: Generic Power Port</li>
</ul></li>
<li>Family: Port Channel, Model: Generic Port Channel</li>
</ul></li>
</ul>

<h4><a id="user-content-family-rules" class="anchor" href="#family-rules" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Family Rules</h4>

<table><thead>
<tr>
<th>Family</th>
<th>Rules</th>
</tr>
</thead><tbody>
<tr>
<td>Firewall</td>
<td>Searchable</td>
</tr>
<tr>
<td>Chassis</td>
<td>Searchable</td>
</tr>
<tr>
<td>Module</td>
<td>Searchable</td>
</tr>
<tr>
<td>Sub Module</td>
<td>Searchable</td>
</tr>
<tr>
<td>Port</td>
<td>Searchable, Connectable, Locked By Default</td>
</tr>
<tr>
<td>Port Channel</td>
<td>Searchable, Connectable, Locked By Default</td>
</tr>
<tr>
<td>Power Port</td>
<td>Searchable, Connectable, Locked By Default</td>
</tr>
</tbody></table>

<h4><a id="user-content-port-channel-usage" class="anchor" href="#port-channel-usage" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Port Channel Usage</h4>

<p>The Port Channel is a logical entity that allows grouping of several physical ports to create one logical link.
In CloudShell, all the ports configured to the port channel shouldn’t be “physically connected” and instead the port channel resource will be “physically connected”. The names of all the ports configured to the port channel will appear in the “Associated Ports” attribute on the port channel.
Addition or removal of ports from the port channel will require execution of Autoload to update the resource representation in CloudShell and a manual update of the physical connections in CloudShell by the administrator.</p>

<h4><a id="user-content-resource-name-and-address" class="anchor" href="#resource-name-and-address" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Resource Name and Address</h4>

<table><thead>
<tr>
<th>Family</th>
<th>Model</th>
<th>Resource Name</th>
<th>Resource Address</th>
</tr>
</thead><tbody>
<tr>
<td>Firewall</td>
<td>[Vendor] [OS] Firewall</td>
<td>(user defined)</td>
<td>(user defined - IP)</td>
</tr>
<tr>
<td>Chassis</td>
<td>Generic Chassis</td>
<td>Chassis[ID]</td>
<td>CH[ID]</td>
</tr>
<tr>
<td>Module</td>
<td>Generic Module</td>
<td>Module[ID]</td>
<td>MO[ID]</td>
</tr>
<tr>
<td>Sub Module</td>
<td>Generic Sub Module</td>
<td>SubModule[ID]</td>
<td>SM[ID]</td>
</tr>
<tr>
<td>Port</td>
<td>Generic Port</td>
<td>The name of the interface as appears in the device. Any “/” character is replaced with “-“, spaces trimmed.]</td>
<td>PO[ID]</td>
</tr>
<tr>
<td>Port Channel</td>
<td>Generic Port Channel</td>
<td>The name of the interface as appears in the device. Any “/” character is replaced with “-“, spaces trimmed.</td>
<td>PC[ID]</td>
</tr>
<tr>
<td>Power Port</td>
<td>Generic Power Port</td>
<td>PP[ContainerID][ID]</td>
<td>PP[ContainerID][ID]</td>
</tr>
</tbody></table>

<p>Note: The [ID] for each sub-resource is taken from the device itself (corresponds to the names defined in the device).</p>

<h3><a id="user-content-attributes" class="anchor" href="#attributes" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Attributes</h3>

<h4><a id="user-content-guidelines" class="anchor" href="#guidelines" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Guidelines</h4>

<ul>
<li>Attributes which aren’t relevant to a devices won’t be populated by the driver.</li>
<li>All attributes which aren't user-input are "read only"</li>
<li>The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings" and "Available For Abstract Resources" enabled.</li>
<li>It is possible to customize the attribute rules selection after importing the Shell to CloudShell.</li>
<li>Attributes shouldn’t be removed.</li>
<li>Custom attributes should be added only to the root level model.</li>
<li>All attributes are of type String unless mentioned otherwise</li>
</ul>

<h5><a id="user-content-vendor-os-firewall" class="anchor" href="#vendor-os-firewall" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>[Vendor] [OS] Firewall</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>User</td>
<td>String</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Password</td>
<td>Password</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Enable Password</td>
<td>Password</td>
<td>Yes</td>
<td>The enable password is required by some CLI protocols such as Telnet and is required according to the device configuration.</td>
</tr>
<tr>
<td>System Name</td>
<td>String</td>
<td>No</td>
<td>A unique identifier for the device, if exists in the device terminal/os.</td>
</tr>
<tr>
<td>Contact Name</td>
<td>String</td>
<td>No</td>
<td>The name of a contact registered in the device.</td>
</tr>
<tr>
<td>OS Version</td>
<td>String</td>
<td>No</td>
<td>Version of the Operating System.</td>
</tr>
<tr>
<td>Vendor</td>
<td>String</td>
<td>No</td>
<td>The name of the device manufacture.</td>
</tr>
<tr>
<td>Location</td>
<td>String</td>
<td>No</td>
<td>The device physical location identifier. For example Lab1/Floor2/Row5/Slot4.</td>
</tr>
<tr>
<td>Model</td>
<td>String</td>
<td>No</td>
<td>The device model. This information is typically used for abstract resource filtering.</td>
</tr>
<tr>
<td>SNMP Read Community</td>
<td>Password</td>
<td>Yes</td>
<td>The SNMP Read-Only Community String is like a password. It is sent along with each SNMP Get-Request and allows (or denies) access to device.</td>
</tr>
<tr>
<td>SNMP Write Community</td>
<td>Password</td>
<td>Yes</td>
<td>The SNMP Write Community String is like a password. It is sent along with each SNMP Set-Request and allows (or denies) chaning MIBs values.</td>
</tr>
<tr>
<td>SNMP V3 User</td>
<td>String</td>
<td>Yes</td>
<td>Relevant only in case SNMP V3 is in use.</td>
</tr>
<tr>
<td>SNMP V3 Password</td>
<td>Password</td>
<td>Yes</td>
<td>Relevant only in case SNMP V3 is in use.</td>
</tr>
<tr>
<td>SNMP V3 Private Key</td>
<td>String</td>
<td>Yes</td>
<td>Relevant only in case SNMP V3 is in use.</td>
</tr>
<tr>
<td>SNMP Version</td>
<td>String</td>
<td>Yes</td>
<td>The version of SNMP to use. Possible values are v1, v2c and v3.</td>
</tr>
<tr>
<td>Console Server IP Address</td>
<td>String</td>
<td>Yes</td>
<td>The IP address of the console server, in IPv4 format.</td>
</tr>
<tr>
<td>Console User</td>
<td>String</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Console Port</td>
<td>Numeric</td>
<td>Yes</td>
<td>The port on the console server, usually TCP port, which the device is associated with.</td>
</tr>
<tr>
<td>Console Password</td>
<td>Password</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>CLI Connection Type</td>
<td>Lookup</td>
<td>Yes</td>
<td>The CLI connection type that will be used by the driver. Possible values are Auto, Console, SSH, Telnet and TCP. If Auto is selected the driver will choose the available connection type automatically. Default value is Auto.</td>
</tr>
<tr>
<td>Power Management</td>
<td>Boolean</td>
<td>Yes</td>
<td>Used by the power management orchestration, if enabled, to determine whether to automatically manage the device power status. Enabled by default.</td>
</tr>
<tr>
<td>Backup Location</td>
<td>String</td>
<td>Yes</td>
<td>The location in which configuration files will be saved in case no backup location input is passed to the Save command.</td>
</tr>
<tr>
<td>Sessions Concurrency Limit</td>
<td>Numeric</td>
<td>Yes</td>
<td>The maximum number of concurrent sessions that the driver will open to the device. Default is 1 (no concurrency).</td>
</tr>
<tr>
<td>CLI TCP Port</td>
<td>String</td>
<td>Yes</td>
<td>TCP Port to user for CLI connection. If kept empty a default CLI port will be used based on the chosen protocol, for example Telnet will use port 23.</td>
</tr>
<tr>
<td>Enable SNMP</td>
<td>Boolean</td>
<td>Yes</td>
<td>If set to True and SNMP isn’t enabled yet in the device the Shell will automatically enable SNMP in the device when Autoload command is called. SNMP must be enabled on the device for the Autoload command to run successfully. True by default.</td>
</tr>
<tr>
<td>Disable SNMP</td>
<td>Boolean</td>
<td>Yes</td>
<td>If set to True SNMP will be disabled automatically by the Shell after the Autoload command execution is completed. False by default.</td>
</tr>
</tbody></table>

<h5><a id="user-content-generic-chassis" class="anchor" href="#generic-chassis" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Chassis</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Model</td>
<td>String</td>
<td>No</td>
<td>The device model. This information is typically used for abstract resource filtering.</td>
</tr>
<tr>
<td>Serial Number</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
</tbody></table>

<h5><a id="user-content-generic-module" class="anchor" href="#generic-module" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Module</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Model</td>
<td>String</td>
<td>No</td>
<td>The device model. This information is typically used for abstract resource filtering.</td>
</tr>
<tr>
<td>Version</td>
<td>String</td>
<td>No</td>
<td>The firmware version of the resource.</td>
</tr>
<tr>
<td>Serial Number</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
</tbody></table>

<h5><a id="user-content-generic-sub-module" class="anchor" href="#generic-sub-module" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Sub Module</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Model</td>
<td>String</td>
<td>No</td>
<td>The device model. This information is typically used for abstract resource filtering.</td>
</tr>
<tr>
<td>Version</td>
<td>String</td>
<td>No</td>
<td>The firmware version of the resource.</td>
</tr>
<tr>
<td>Serial Number</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
</tbody></table>

<h5><a id="user-content-generic-port" class="anchor" href="#generic-port" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Port</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>MAC Address</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>L2 Protocol Type</td>
<td>String</td>
<td>No</td>
<td>The L2 protocol type configured on the interface. For example POS, Serial.</td>
</tr>
<tr>
<td>IPv4 Address</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>IPv6 Address</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>Port Description</td>
<td>String</td>
<td>No</td>
<td>The description of the port as configured in the device.</td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Numeric</td>
<td>No</td>
<td>The current interface bandwidth, in MB.</td>
</tr>
<tr>
<td>MTU</td>
<td>Numeric</td>
<td>No</td>
<td>The current MTU configured on the interface.</td>
</tr>
<tr>
<td>Duplex</td>
<td>Lookup</td>
<td>No</td>
<td>The current duplex configuration on the interface. Possible values are Half or Full.</td>
</tr>
<tr>
<td>Adjacent</td>
<td>String</td>
<td>No</td>
<td>The adjacent device (system name) and port, based on LLDP or CDP protocol.</td>
</tr>
<tr>
<td>Auto Negotiation</td>
<td>Boolean</td>
<td>No</td>
<td>The current auto negotiation configuration on the interface.</td>
</tr>
</tbody></table>

<h5><a id="user-content-generic-port-channel" class="anchor" href="#generic-port-channel" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Port Channel</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Associated Ports</td>
<td>String</td>
<td>No</td>
<td>Ports associated with this port channel. The value is in the format “[portResourceName],…”, for example “GE0-0-0-1,GE0-0-0-2”</td>
</tr>
<tr>
<td>IPv4 Address</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>IPv6 Address</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>Port Description</td>
<td>String</td>
<td>No</td>
<td>The description of the port as configured in the device.</td>
</tr>
</tbody></table>

<h5><a id="user-content-generic-power-port" class="anchor" href="#generic-power-port" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Generic Power Port</h5>

<table><thead>
<tr>
<th>Attribute Name</th>
<th>Data Type</th>
<th>User input?</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Model</td>
<td>String</td>
<td>No</td>
<td>The device model. This information is typically used for abstract resource filtering.</td>
</tr>
<tr>
<td>Serial Number</td>
<td>String</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>Version</td>
<td>String</td>
<td>No</td>
<td>The firmware version of the resource.</td>
</tr>
<tr>
<td>Port Description</td>
<td>String</td>
<td>No</td>
<td>The description of the port as configured in the device.</td>
</tr>
</tbody></table>

<h2><a id="user-content-commands" class="anchor" href="#commands" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Commands</h2>

<p>Below is a list of all the commands that will be part of the standard Shell, their names and interfaces. Each firewall Shell that will be released by Quali’s engineering will include implementation for all those commands.</p>

<p>When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.</p>

<p>Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output. The “Autoload” command has a special output on success that CloudShell reads when building the resource hierarchy. The “Save” command will return an output on success with the file name (exact syntax below).</p>

<p>Note that the connectivity ApplyConnectivityChanges command behaves differently between Switches and Routers. In Switches, the ApplyConnectivityChanges command can configure VLAN Access or VLAN Trunk on a port, or clear the VLAN configuration from the port. In Routers, the ApplyConnectivityChanges command creates a sub-interface (which isn't modeled in CloudShell) on the port which allows traffic with the specified VLAN tags (both outer and inner) to pass via this port. Clearing the VLAN configuration from a port in a Router translates to removal of the sub-interfaces. This means that a device which is directly connected to a router can be connected only to VLAN service of type Trunk in CloudShell.</p>

<h3><a id="user-content-autoload" class="anchor" href="#autoload" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Autoload</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">get_inventory</span> (<span class="pl-smi"><span class="pl-smi">self</span></span>, <span class="pl-smi">context</span>)</pre></div>

<h6><a id="user-content-description" class="anchor" href="#description" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>This function queries the device, discovers it's specification and structure and autoload it into CloudShell. When new resource is created Cloudshell asks the user to specify some user input (i.e user name &amp; psasword) and then it calls the get_inventory function.</p>

<h6><a id="user-content-notes" class="anchor" href="#notes" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>The standard recommended way of communicating and discovering the device is via SNMP protocol and therefore this command requires SNMP to be configured in the device. In case SNMP isn’t configured in the device and the attribute “Enable SNMP” on the root model is set to True the Autoload command will configure SNMP in the device. If the attribute “Disable SNMP” on the root model is set to True the Autoload command will disable the SNMP in the device once the discovery of the device is completed. In case SNMP isn't configured and "Enable SNMP" on the root model is set to false a relevant error message will be displayed.</p>

<h6><a id="user-content-display-name" class="anchor" href="#display-name" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>System command, it has no display name</p>

<h6><a id="user-content-parameters" class="anchor" href="#parameters" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>context</td>
<td>-</td>
<td>object</td>
<td>system parameter</td>
<td>object of type AutoLoadCommandContext which includes API connectivity details and the details of the resource including attributes that the user entered during the resource creation.</td>
</tr>
<tr>
<td>Output</td>
<td>AutoLoadDetails</td>
<td>-</td>
<td>object</td>
<td>Yes</td>
<td>object of type AutoLoadDetails with the discovered resource structure and attributes.</td>
</tr>
</tbody></table>

<h3><a id="user-content-save" class="anchor" href="#save" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Save</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">save</span> (<span class="pl-smi">folder_path</span>, <span class="pl-smi">configuration_type</span>)</pre></div>

<h6><a id="user-content-description-1" class="anchor" href="#description-1" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Create and save a configuration file</p>

<h6><a id="user-content-display-name-1" class="anchor" href="#display-name-1" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Save</p>

<h6><a id="user-content-parameters-1" class="anchor" href="#parameters-1" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>folder_path</td>
<td>Folder Path</td>
<td>string</td>
<td>No</td>
<td>The path in which the configuration file will be saved. Won't include the name of the file but only the folder. This input is optional and in case this input is empty the value will be taken from the "Backup Location" attribute on the root resource. The path should include the protocol type, for TFTP use "tftp://asdf", for FTP use "ftp://username:password@server_address/folder1/file1.bin".</td>
</tr>
<tr>
<td>Input</td>
<td>configuration_type</td>
<td>Configuration Type</td>
<td>string</td>
<td>No</td>
<td>The type of configuration that will be saved. Possible values are StartUp and Running. If kept empty the default configuration type that will be used is Running.</td>
</tr>
<tr>
<td>Output</td>
<td></td>
<td></td>
<td>string</td>
<td>Yes</td>
<td>. The configuration file name should be “[ResourceName]-[ConfigurationType]-[DDMMYY]-[HHMMSS]”.</td>
</tr>
</tbody></table>

<h3><a id="user-content-restore" class="anchor" href="#restore" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Restore</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">restore</span> (<span class="pl-smi">path</span>, <span class="pl-smi">configuration_type</span>, <span class="pl-smi">restore_method</span>)</pre></div>

<h6><a id="user-content-description-2" class="anchor" href="#description-2" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Restore a configuration file</p>

<h6><a id="user-content-display-name-2" class="anchor" href="#display-name-2" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Restore</p>

<h6><a id="user-content-parameters-2" class="anchor" href="#parameters-2" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>path</td>
<td>Path</td>
<td>string</td>
<td>Yes</td>
<td>The path to the configuration file, including the configuration file name. The path should include the protocol type, for TFTP use "tftp://asdf", for FTP use "ftp://username:password@server_address/folder1/file1.bin".</td>
</tr>
<tr>
<td>Input</td>
<td>configuration_type</td>
<td>Configuration Type</td>
<td>string</td>
<td>No</td>
<td>The configuration type to restore. Possible values are StartUp and Running. If kept empty the configuration type that will be restored is Running.</td>
</tr>
<tr>
<td>Input</td>
<td>restore_method</td>
<td>Restore Method</td>
<td>string</td>
<td>No</td>
<td>The restore method to use when restoring the configuration file. Possible Values are Append and Override. If kept empty the restore method will be Override.</td>
</tr>
</tbody></table>

<h3><a id="user-content-load-firmware" class="anchor" href="#load-firmware" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Load Firmware</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">load_firmware</span> (<span class="pl-smi">path</span>)</pre></div>

<h6><a id="user-content-description-3" class="anchor" href="#description-3" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Loads a firmware onto the device</p>

<h6><a id="user-content-notes-1" class="anchor" href="#notes-1" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>This command is CLI based and applies to the whole device, also in case of multi-chassis device.</p>

<h6><a id="user-content-display-name-3" class="anchor" href="#display-name-3" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Load Firmware</p>

<h6><a id="user-content-parameters-3" class="anchor" href="#parameters-3" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>path</td>
<td>Path</td>
<td>string</td>
<td>Yes</td>
<td>The path to the firmware file, including the firmware file name. The path should include the protocol type, for TFTP use "tftp://asdf", for FTP use "ftp://username:password@server_address/folder1/file1.bin".</td>
</tr>
</tbody></table>

<h3><a id="user-content-run-custom-command" class="anchor" href="#run-custom-command" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Run Custom Command</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">run_custom_command</span> (<span class="pl-smi">custom_command</span>)</pre></div>

<h6><a id="user-content-description-4" class="anchor" href="#description-4" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Executes any custom command entered in the input on the device.</p>

<h6><a id="user-content-display-name-4" class="anchor" href="#display-name-4" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Run Custom Command</p>

<h6><a id="user-content-parameters-4" class="anchor" href="#parameters-4" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>custom_command</td>
<td>Custom Command</td>
<td>string</td>
<td>Yes</td>
<td>The command to execute. Note that commands that require a reponse aren't supported.</td>
</tr>
</tbody></table>

<h3><a id="user-content-run-custom-config-command" class="anchor" href="#run-custom-config-command" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Run Custom Config Command</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">run_custom_command</span> (<span class="pl-smi">custom_command</span>)</pre></div>

<h6><a id="user-content-description-5" class="anchor" href="#description-5" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Executes any custom config command entered in the input on the device.</p>

<h6><a id="user-content-notes-2" class="anchor" href="#notes-2" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>This command should be hidden from the UI.</p>

<h6><a id="user-content-display-name-5" class="anchor" href="#display-name-5" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Run Custom Config Command</p>

<h6><a id="user-content-parameters-5" class="anchor" href="#parameters-5" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>custom_command</td>
<td>Custom Command</td>
<td>string</td>
<td>Yes</td>
<td>The command to execute. Note that commands that require a reponse aren't supported.</td>
</tr>
</tbody></table>

<h3><a id="user-content-shutdown" class="anchor" href="#shutdown" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Shutdown</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">shutdown</span>()</pre></div>

<h6><a id="user-content-description-6" class="anchor" href="#description-6" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Sends a graceful shutdown to the device.</p>

<h6><a id="user-content-notes-3" class="anchor" href="#notes-3" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>Not all devices support a shutdown command. In such cases the command just won’t be implemented.</p>

<h6><a id="user-content-display-name-6" class="anchor" href="#display-name-6" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Shutdown</p>

<h6><a id="user-content-parameters-6" class="anchor" href="#parameters-6" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<p>No input parameters.</p>

<h3><a id="user-content-health-check" class="anchor" href="#health-check" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Health Check</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">health_check</span>()</pre></div>

<h6><a id="user-content-description-7" class="anchor" href="#description-7" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Description</h6>

<p>Performs checks on the device that validates that the Shell can work. In a firewall device this checks usually include connectivity check for the protocols used by the Shell. The healtcheck result will be visible in the resource live status and command output.</p>

<h6><a id="user-content-notes-4" class="anchor" href="#notes-4" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>In case the performed checks fail the live status of the resource should be "Error" and both the live status description and the output of the command should be "Health check on resource [root_resource_name] failed".
In case all performed checks passed the live status of the resource should be "Online" and both the live status description and the output of the command should be "Health check on resource [root_resource_name] passed".
CLI check is the check that is currently supported by the networking devices.</p>

<h6><a id="user-content-display-name-7" class="anchor" href="#display-name-7" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>Health Check</p>

<h6><a id="user-content-parameters-7" class="anchor" href="#parameters-7" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Output</td>
<td></td>
<td></td>
<td>string</td>
<td>Yes</td>
<td>The health check result</td>
</tr>
</tbody></table>

<h3><a id="user-content-orchestration_save" class="anchor" href="#orchestration_save" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>orchestration_save</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">orchestration_save</span>(<span class="pl-smi">mode</span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">"</span>shallow<span class="pl-pds">"</span></span>, <span class="pl-smi">custom_params</span> <span class="pl-k">=</span> null)</pre></div>

<h6><a id="user-content-notes-5" class="anchor" href="#notes-5" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>Based on the Orchestration Save and Restore Standard - <a href="https://github.com/QualiSystems/sandbox_orchestration_standard/blob/master/save%20%26%20restore/save%20%26%20restore%20standard.md">https://github.com/QualiSystems/sandbox_orchestration_standard/blob/master/save%20%26%20restore/save%20%26%20restore%20standard.md</a>
The command wraps the Save command with a standard interface that will be used by the Sandbox orchestration. This command will call the Save command which will create a configuration file.
The command should be hidden from the UI.
In case there is no folder_path input and the attribute "Backup Location" on the root model is empty the command should throw an error.</p>

<h6><a id="user-content-display-name-8" class="anchor" href="#display-name-8" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>orchestration_save</p>

<h6><a id="user-content-parameters-8" class="anchor" href="#parameters-8" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>mode</td>
<td>mode</td>
<td>string</td>
<td>Yes</td>
<td>The save mode. Possible values are "Shallow" and "Deep". In a firewall device both modes will have the same behavior of saving a configuration file.</td>
</tr>
<tr>
<td>Input</td>
<td>custom_params</td>
<td>custom_params</td>
<td>string</td>
<td>Yes</td>
<td>A JSON data structure with optional parameters. If no parameters are passed the defaults defined on the root resource and in the Save command will be used.</td>
</tr>
<tr>
<td>Output</td>
<td>saved_artifact_info</td>
<td>saved_artifact_info</td>
<td>string</td>
<td>Yes</td>
<td>A composite data structure that represents the details of the snapshot.</td>
</tr>
</tbody></table>

<p>An example for the "custom_params" input:</p>

<div class="highlight highlight-source-json"><pre>{
  <span class="pl-s"><span class="pl-pds">"</span>custom_params<span class="pl-pds">"</span></span>: {
    <span class="pl-s"><span class="pl-pds">"</span>configuration_type<span class="pl-pds">"</span></span> : <span class="pl-s"><span class="pl-pds">"</span>StartUp<span class="pl-pds">"</span></span>
    <span class="pl-s"><span class="pl-pds">"</span>folder_path<span class="pl-pds">"</span></span> <span class="pl-ii">:</span> <span class="pl-s"><span class="pl-pds">"</span>tftp://10.0.0.1/folder1<span class="pl-pds">"</span></span>
  }
}</pre></div>

<p>An example for the "saved_artifact_info" output:</p>

<div class="highlight highlight-source-json"><pre>{
  <span class="pl-s"><span class="pl-pds">"</span>saved_artifact_info<span class="pl-pds">"</span></span>: {
    <span class="pl-s"><span class="pl-pds">"</span>resource_name<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>CiscoNXOSSwitch1<span class="pl-pds">"</span></span>,
    <span class="pl-s"><span class="pl-pds">"</span>resource_id<span class="pl-pds">"</span></span> : <span class="pl-s"><span class="pl-pds">"</span>5F2EAA6C-E3FD-4DF0-8E2D-F05C81D61631<span class="pl-pds">"</span></span>,
    <span class="pl-s"><span class="pl-pds">"</span>created_date<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>3577-04-27T00:17:48.819Z<span class="pl-pds">"</span></span>,
    <span class="pl-s"><span class="pl-pds">"</span>restore_rules<span class="pl-pds">"</span></span>: {
      <span class="pl-s"><span class="pl-pds">"</span>requires_same_resource<span class="pl-pds">"</span></span>: <span class="pl-c1">true</span>
    },    
    <span class="pl-s"><span class="pl-pds">"</span>saved_artifact<span class="pl-pds">"</span></span> :{
      <span class="pl-s"><span class="pl-pds">"</span>artifact_type<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>tftp<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>identifier<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>/folder1/CiscoNXOSSwitch1-Running-080816-13:20:53<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>server<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>server1<span class="pl-pds">"</span></span>
    }
  }
}</pre></div>

<p>The artifact types supported by firewall orchestration_save command are "ftp", "tftp" and "filesystem".
The "requires_same_resource" restore rule for firewall devices is always True.</p>

<h3><a id="user-content-orchestration_restore" class="anchor" href="#orchestration_restore" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>orchestration_restore</h3>

<div class="highlight highlight-source-python"><pre><span class="pl-k">def</span> <span class="pl-en">orchestration_restore</span>(<span class="pl-smi">saved_artifact_info</span>, <span class="pl-smi">custom_params</span> <span class="pl-k">=</span> null)</pre></div>

<h6><a id="user-content-notes-6" class="anchor" href="#notes-6" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Notes</h6>

<p>Based on the Orchestration Save and Restore Standard - <a href="https://github.com/QualiSystems/sandbox_orchestration_standard/blob/master/save%20%26%20restore/save%20%26%20restore%20standard.md">https://github.com/QualiSystems/sandbox_orchestration_standard/blob/master/save%20%26%20restore/save%20%26%20restore%20standard.md</a>
The command wraps the Restore command with a standard interface that will be used by the Sandbox orchestration. This command will call the Save command which will create a configuration file.
The command should be hidden from the UI.
In case the saved artifact type is FTP the FTP credentials are saved on the FTP resource, so the orchestration_restore command will access the FTP resource to get them and pass them to the Restore command.</p>

<h6><a id="user-content-display-name-9" class="anchor" href="#display-name-9" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Display Name</h6>

<p>orchestration_restore</p>

<h6><a id="user-content-parameters-9" class="anchor" href="#parameters-9" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Parameters</h6>

<table><thead>
<tr>
<th>Input / Output</th>
<th>Parameter</th>
<th>Alias</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead><tbody>
<tr>
<td>Input</td>
<td>saved_artifact_info</td>
<td>saved_artifact_info</td>
<td>string</td>
<td>Yes</td>
<td>A composite data structure that represents the details of the snapshot. The value that will be passed as input must be the same as the exact value that the save function returned.</td>
</tr>
<tr>
<td>Input</td>
<td>custom_params</td>
<td>custom_params</td>
<td>string</td>
<td>Yes</td>
<td>A JSON data structure with optional parameters. If no parameters are passed the defaults defined on the root resource and in the Restore command will be used.</td>
</tr>
</tbody></table>

<p>An example for the "custom_params" input:</p>

<div class="highlight highlight-source-json"><pre>{
  <span class="pl-s"><span class="pl-pds">"</span>custom_params<span class="pl-pds">"</span></span>: {
    <span class="pl-s"><span class="pl-pds">"</span>path<span class="pl-pds">"</span></span> : <span class="pl-s"><span class="pl-pds">"</span>tftp://10.0.0.1/folder1<span class="pl-pds">"</span></span>
    <span class="pl-s"><span class="pl-pds">"</span>restore_method<span class="pl-pds">"</span></span> <span class="pl-ii">:</span> <span class="pl-s"><span class="pl-pds">"</span>Append<span class="pl-pds">"</span></span>
    <span class="pl-s"><span class="pl-pds">"</span>configuration_type<span class="pl-pds">"</span></span> <span class="pl-ii">:</span> <span class="pl-s"><span class="pl-pds">"</span>StartUp<span class="pl-pds">"</span></span>
  }
}</pre></div>

<p>An example for the "saved_artifact_info" input:</p>

<div class="highlight highlight-source-json"><pre>{
  <span class="pl-s"><span class="pl-pds">"</span>saved_artifact_info<span class="pl-pds">"</span></span>: {
    <span class="pl-s"><span class="pl-pds">"</span>resource_name<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>CiscoASAFirewall1<span class="pl-pds">"</span></span>,
    <span class="pl-s"><span class="pl-pds">"</span>resource_id<span class="pl-pds">"</span></span> : <span class="pl-s"><span class="pl-pds">"</span>5F2EAA6C-E3FD-4DF0-8E2D-F05C81D61631<span class="pl-pds">"</span></span>,
    <span class="pl-s"><span class="pl-pds">"</span>created_date<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>3577-04-27T00:17:48.819Z<span class="pl-pds">"</span></span>,
    <span class="pl-s"><span class="pl-pds">"</span>restore_rules<span class="pl-pds">"</span></span>: {
      <span class="pl-s"><span class="pl-pds">"</span>requires_same_resource<span class="pl-pds">"</span></span>: <span class="pl-c1">true</span>
    },    
    <span class="pl-s"><span class="pl-pds">"</span>saved_artifact<span class="pl-pds">"</span></span> :{
      <span class="pl-s"><span class="pl-pds">"</span>artifact_type<span class="pl-pds">"</span></span> : <span class="pl-s"><span class="pl-pds">"</span>ftp<span class="pl-pds">"</span></span>,
      <span class="pl-s"><span class="pl-pds">"</span>ftp_resource<span class="pl-pds">"</span></span> : <span class="pl-s"><span class="pl-pds">"</span>ftp_srv1<span class="pl-pds">"</span></span>, 
      <span class="pl-s"><span class="pl-pds">"</span>identifier<span class="pl-pds">"</span></span>: <span class="pl-s"><span class="pl-pds">"</span>/folder1/CiscoNXOSSwitch1-Running-080816-13:20:53<span class="pl-pds">"</span></span>
    }
  }
}</pre></div>

<p>The artifact types supported by firewall orchestration_restore command are "ftp", "tftp" and "filesystem".
The "requires_same_resource" restore rule for firewall devices is always True.</p>
</article>
  </div>

</div>

<button type="button" data-facebox="#jump-to-line" data-facebox-class="linejump" data-hotkey="l" class="d-none">Jump to Line</button>
<div id="jump-to-line" style="display:none">
  <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="" class="js-jump-to-line-form" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <input class="form-control linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
    <button type="submit" class="btn">Go</button>
</form></div>

  </div>
  <div class="modal-backdrop js-touch-events"></div>
</div>


    </div>
  </div>

    </div>

        <div class="container site-footer-container">
  <div class="site-footer" role="contentinfo">
    <ul class="site-footer-links float-right">
        <li><a href="https://github.com/contact" data-ga-click="Footer, go to contact, text:contact">Contact GitHub</a></li>
      <li><a href="https://developer.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
      <li><a href="https://shop.github.com" data-ga-click="Footer, go to shop, text:shop">Shop</a></li>
        <li><a href="https://github.com/blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a href="https://github.com/about" data-ga-click="Footer, go to about, text:about">About</a></li>

    </ul>

    <a href="https://github.com" aria-label="Homepage" class="site-footer-mark" title="GitHub">
      <svg aria-hidden="true" class="octicon octicon-mark-github" height="24" version="1.1" viewBox="0 0 16 16" width="24"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>
    <ul class="site-footer-links">
      <li>&copy; 2017 <span title="0.09460s from github-fe155-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
        <li><a href="https://github.com/site/terms" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li><a href="https://github.com/site/privacy" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li><a href="https://github.com/security" data-ga-click="Footer, go to security, text:security">Security</a></li>
        <li><a href="https://status.github.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
        <li><a href="https://help.github.com" data-ga-click="Footer, go to help, text:help">Help</a></li>
    </ul>
  </div>
</div>



    

    <div id="ajax-error-message" class="ajax-error-message flash flash-error">
      <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"/></svg>
      <button type="button" class="flash-close js-flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
        <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
      </button>
      You can't perform that action at this time.
    </div>


      
      <script crossorigin="anonymous" integrity="sha256-0j4y5IIRK6Xj6pvY3H5VVoARanTgAnRqyR9BpOWHWps=" src="https://assets-cdn.github.com/assets/frameworks-d23e32e482112ba5e3ea9bd8dc7e555680116a74e002746ac91f41a4e5875a9b.js"></script>
      <script async="async" crossorigin="anonymous" integrity="sha256-DeRGyzdl03caIB25OS+rzBwVlt3Yio4iDy83c8zBL50=" src="https://assets-cdn.github.com/assets/github-0de446cb3765d3771a201db9392fabcc1c1596ddd88a8e220f2f3773ccc12f9d.js"></script>
      
      
      
      
    <div class="js-stale-session-flash stale-session-flash flash flash-warn flash-banner d-none">
      <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"/></svg>
      <span class="signed-in-tab-flash">You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
      <span class="signed-out-tab-flash">You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
    </div>
    <div class="facebox" id="facebox" style="display:none;">
  <div class="facebox-popup">
    <div class="facebox-content" role="dialog" aria-labelledby="facebox-header" aria-describedby="facebox-description">
    </div>
    <button type="button" class="facebox-close js-facebox-close" aria-label="Close modal">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
    </button>
  </div>
</div>

  </body>
</html>

