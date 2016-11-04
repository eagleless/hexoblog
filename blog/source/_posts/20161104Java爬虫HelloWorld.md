---
title: Java爬虫HelloWorld
date: 2016-11-04 18:00:22
tags: [splide]
---
使用爬虫获取产品信息。
<!--more-->

#   jar包坐标

    <dependency>
        <groupId>org.jsoup</groupId>
        <artifactId>jsoup</artifactId>
        <version>1.9.2</version>
    </dependency>

#   简单实例

获取产品信息，根据一定的条件，选择优质债权发送给指定邮箱。

```java
Timer timer = new Timer();
timer.schedule( new TimerTask() {
    @Override
    public void run() {
        System.out.println(DateTool.format( new Date(),"yyyy-MM-dd HH:mm:ss" ));
        try {
            String url = "https://xinghuo.yixin.com/wuqing?category=12";
            Document doc = Jsoup.connect(url).get();
            Elements els = doc.getElementsByClass("ui-bg-color");
            StringBuffer sb = new StringBuffer();
            for(Iterator<Element> es = els.iterator();es.hasNext();){
                Element e = es.next();
                String info = e.text();
                String[] infos = info.split( " " ) ;
                Double a = Double.valueOf( infos[1].replaceAll( "%", "" ) ) ;
                Integer rundays = Integer.valueOf( infos[3].replaceAll( "天", "" ) );
                Double result = rundays/a;
                if(result < 42){
                    sb.append( "【"+infos[0] +"】收益率为" + infos[1]+",当前剩余配额【"+infos[4]+"】,投资天数【"+infos[3]+"】\n");
                }
            }
            if(sb!=null && sb.length()>0){
                JmsTool.sendMultipartEmail( "变现贷好产品提醒", "kaiyang12@creditease.cn", null, sb.toString() );
            }
        } catch ( IOException e ) {
            e.printStackTrace();
        }
    }
}, 60000*5,60000*5);
```
