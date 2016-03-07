title: wp实现图片动态自动切换
categories:
  - WP8
date: 2013-08-12 13:13:21
tags:
  - WP8
---

    ``` 
           Storyboard  timer = new Storyboard();
            timer.Duration = TimeSpan.FromMilliseconds(3000);
            timer.Completed += new EventHandler(timer_Completed);
            timer.Begin();
          int i=0;
         /// <summary>
        /// 图片自动切换
        /// </summary>
        public void changeBackground()
        {
            if (WebServiceCall.imageList.Count == 0)
            {
                return;
            }
            selectNewsId = WebServiceCall.imageList[i].NewsId;//存储新闻ID
            title.Text = news.StringTruncat(WebServiceCall.imageList[i].NewsTitle, 15, "...");
            newsTitle = WebServiceCall.imageList[i].NewsTitle;
            ImageBrush bursh = new ImageBrush();
            bursh.ImageSource = new BitmapImage(new Uri(WebServiceCall.imageList[i].ImageUrl, UriKind.Absolute));
            myImage.Background = bursh;
            //  this.pb1.Image = WebServiceCall.imageList[i];
            i++;
            if (i == WebServiceCall.imageList.Count)
            {
                i = 0;
            }
        }
        void timer_Completed(object sender, EventArgs e)
        {
            changeBackground();
            timer.Begin();
        }
```