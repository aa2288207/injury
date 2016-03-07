title: wp实现刷新本页面
categories:
  - WP8
date: 2013-08-12 09:50:50
tags:
  - WP8
---

   NavigationService.Navigate(new Uri("/NewsListPage.xaml" + "?Refresh=" + Guid.NewGuid(), UriKind.Relative));