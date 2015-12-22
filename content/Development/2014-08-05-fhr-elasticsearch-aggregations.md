title: What’s the Filthiest PostCode in UK? and the Cleanest too!
date: 2014-08-05
slug: /2014/08/05/fhr-elasticsearch-aggregations/
tags: Development, Java, elasticsearch, github

There&#8217;s a [GitHub repo][1] associated to this post that [it can be found here][1]

Do you know that sticker on the window of most takeaway shops? that sticker displays the Hygiene rating. This post is not about those stickers.

<img class="aligncenter size-full wp-image-303" src="http://ivan.pedrazas.me/wp-content/uploads/2014/08/fhrs_5_en-gb.jpg" alt="Hygiene Rating Sticker" width="290" height="148" />

Now, as it happens, restaurants, deli bars and of course, take away shops are checked up regularly to see how clean are they and the collected information ends up in a report, a sticker and&#8230; some dark and remote database.

After doing the ElastiSearch training three weeks ago I was itching to do some aggregations with it. I have done aggregations before using &#8220;_Ye Olde_&#8221; Map/Reduce approach and I was interested on seeing how it would compare to do agregations with MongoDB.

I found the Food and Higiene dataset and a python script later I had all their data in my hard drive (just under 500MB of XMLs). Since I like diversity, I wrote a Java program to parse those XMLs and add them into my ElasticSearch instance. It really surprised me the amount of time spent on preparing the data before being able to execute the analysis. I know, it shouldn&#8217;t but it does&#8230; every single time it does.

Anyway, I run ElasticSearch in a docker instance that has the Marvel plugin in it. This plugin is perfect for throwing a few quick queries and getting some json back. Of course, me being me, I could not just do some tests and write a blog post&#8230; I had to create [a Github Repo][1] where you can find the source code (just in case you do want to try it by yourself), results (in json files) and some more detailed explanation about how to fetch the data, run the docker container and the different queries I issued.

After indexing almost half a Gigabyte I discovered that the average rating In UK for Food Hygiene is **3.5849** which is not that great, is it? I mean, we are talking about how clean is the place where we eat: &#8220;kind of not clean but not dirty neither&#8221;.

What else did I find? Well, I was interested on my area (NW10) average: **3.23910171730515  **Depressing, I guess it&#8217;s time to move to&#8230; where?

Well, let&#8217;s find out, what&#8217;s the cleanest Post Code? I didn&#8217;t know much about UK PostCodes. Post Code indicates the area (outward) and the building/house (inward). The dataset provides longitude and latitude for every single establishment so you don&#8217;t really need the PostCode to put the stablishment in a map. Anyway, that was not my intention.

So, as it turns, the cleanest Post Code is [SOUTH PETHERTON (TA13)][2], or if you think that 42 establishments and an average of **4.761904761904762** is not significant enough I can move to [TAUNTON (TA3)][3] with a wooping average of **4.642857142857143**

And now that we know where to go, which place we should all avoid? Ladies and Gentlemen, the filthiest area in UK is (shame on you)&#8230;

[HAWICK, NEWCASTLETON (TD9)][4] with a terrible average of **0.013761467889908258** (yes, that&#8217;s Zero point Zero One).

<pre>{
   "key": "td9",
   "doc_count": 218,
   "avg_height": {
      "value": 0.013761467889908258
   }
},

 {
   "key": "ta13",
   "doc_count": 42,
   "avg_height": {
      "value": 4.761904761904762
   }
},
{
   "key": "ta3",
   "doc_count": 112,
   "avg_height": {
      "value": 4.642857142857143
   }
},
</pre>

But let&#8217;s not stop there&#8230; What is the most common rating? XX

The Food Standars Agency has a web form that let&#8217;s you check the rating of your favourite place.

Let me show you one of the queries I used, just in case you&#8217;re looking at how to do aggregations with ElasticSearch and are struggling with the lack of documentation:

<pre>GET _search
{

   "query" : {
      "match" : { "PostCode" : "PO18*"}
       },
   "aggs" : {
        "Food_hygiene_ratings" : {
           "terms" : {
             "field" : "RatingValue"
           }
        },

        "avg_height" : {
          "avg" : {
            "field" : "RatingValue" }

        }
      }
}
</pre>

This query matches a PostCode (PO18 ) and then it aggregates twice the result using the field RatingValue. The first one will give you the count of the different ratings and the second one will give you the average of the rating.

Conclusion? prepating the data was quiet of a pain, but it always is. Loading the data was blazing fast and the results were pretty quick too. The aggregation of all the PostCodes took a few seconds and the huge amount of data that it returned was impressive.

All in all, a very quick way of getting some json data to feed into the D3 visualisations.

[http://en.wikipedia.org/wiki/List\_of\_postcode\_areas\_in\_the\_United_Kingdom][5]

<pre>GET _search
{

   "aggs" : {
        "Food_hygiene_ratings" : {
           "terms" : {
             "field" : "areacode",
             "size": 0,
             "order": {
                    "avg_height": "desc"
                }

           },

           "aggs":{
             "postcodes":{
             "terms" : {
               "field" : "RatingValue"
              }
             }
             ,

        "avg_height" : {
          "avg" : {
            "field" : "RatingValue"

          }

        }
           }
        }
      }
}
</pre>

Once we know the area, we want to filter by outward

**Worst case TD**

<pre>GET _search
{

    "query" : {
      "match" : { "areacode" : "td"}
       },
   "aggs" : {
        "Food_hygiene_ratings" : {
           "terms" : {
             "field" : "outward",
             "size": 0,
             "order": {
                    "avg_height": "desc"
                }

           },

           "aggs":{

              "avg_height" : {
                "avg" : {
                  "field" : "RatingValue"
                }

              }
           }
      }
    }
}

</pre>

**Worst case**

<pre>"key": "td",
   "doc_count": 1492,
   "postcodes": {
      "buckets": [
         {
            "key": 0,
            "key_as_string": "0",
            "doc_count": 1244
         },
         {
            "key": 5,
            "key_as_string": "5",
            "doc_count": 152
         },
         {
            "key": 4,
            "key_as_string": "4",
            "doc_count": 53
         },
         {
            "key": 3,
            "key_as_string": "3",
            "doc_count": 37
         },
         {
            "key": 1,
            "key_as_string": "1",
            "doc_count": 4
         },
         {
            "key": 2,
            "key_as_string": "2",
            "doc_count": 2
         }
      ]
   },
   "avg_height": {
      "value": 0.7312332439678284
   }
},

</pre>

**Best case**

<pre>{
   "key": "ta",
   "doc_count": 2823,
   "postcodes": {
      "buckets": [
         {
            "key": 5,
            "key_as_string": "5",
            "doc_count": 1955
         },
         {
            "key": 4,
            "key_as_string": "4",
            "doc_count": 521
         },
         {
            "key": 3,
            "key_as_string": "3",
            "doc_count": 152
         },
         {
            "key": 0,
            "key_as_string": "0",
            "doc_count": 107
         },
         {
            "key": 1,
            "key_as_string": "1",
            "doc_count": 52
         },
         {
            "key": 2,
            "key_as_string": "2",
            "doc_count": 36
         }
      ]
   },
   "avg_height": {
      "value": 4.406305348919589
   }
},
</pre>

 [1]: https://github.com/ipedrazas/crawlers/tree/master/FHR
 [2]: https://www.google.co.uk/maps/place/South+Petherton,+Somerset+TA13/@50.8277828,-2.2505537,9z/data=!4m2!3m1!1s0x48726c54bfd88a65:0xc91f5b601623f2d1
 [3]: https://www.google.co.uk/maps/place/Taunton,+Somerset/@52.1627957,-1.8741876,7z/data=!4m2!3m1!1s0x486d8a921fb7907f:0x75eb0e344edee9fb
 [4]: https://www.google.co.uk/maps/place/Hawick,+Scottish+Borders+TD9/@53.3002712,-2.738034,7z/data=!4m6!1m3!3m2!1s0x487d796662ced111:0x2cc564208e63c086!2sShankend+Holiday+Cottage+Hawick!3m1!1s0x487d605a6cc3a265:0x188c40d9107d6db6
 [5]: http://en.wikipedia.org/wiki/List_of_postcode_areas_in_the_United_Kingdom
