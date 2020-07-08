---
author: Neel Homchowdhury
date: "2020-04-28"
linktitle: Correlations on Social Media 
menu:
  main:
    parent: tutorials
next: /tutorials/github-pages-blog
prev: /tutorials/automated-deployments
title: Do correlations exist between musical artists and their followers on social media?
weight: 10
---


## Introduction
Current approaches to marketing musicians have changed following the dramatic rise and dominance of online streaming and the prevalence of social media outlets in creating distinct brands. Direct marketing on social media and a comprehensive online presence has become critical to the success of these artists. However, for up and coming artists, breaking finding widespread success has become increasingly difficult due to the sheer volume of new artists that are discoverable on these platforms. I responded to this problem by trying to examine if commonalities existed between the audience of musicians in a similar genre, and whether these characteristics could be utilized to identify up-and-coming musicians. 


## Data Retrieval and Cleaning
I interfaced with Twitter's REST API in order to draw information about 4 up-and-coming artists. These artists chosen were Bakar, Yeek, Dominic Fike, and Omar Apollo. I decided to choose these 4 because they're music all largely fell within the same genre, and all artists had collaborated together on various projects, making it more probable that they had a common follower profile.

Utilizing the Tweepy Package in Python in order to draw the information from Twitter, I wrote 2 functions in order to draw the information:

```python
def get_the_followers(user_name):
    #returns a list of all followers of a twitter account
    
    api = tweepy.API(auth)
    followers = []
    for page in tweepy.Cursor(api.followers, screen_name=user_name, wait_on_rate_limit=True,count=200).pages():
        try:
            followers.extend(page)
        except tweepy.TweepError as e:
            print("Going to sleep:", e)
            time.sleep(60)
    return followers

def get_the_friendships(ids):
    #returns a list of the users a specific twitter account follows
    
    api = tweepy.API(auth)
    final_peeps = []
    for name in ids:
        peeps = []
        for page in tweepy.Cursor(api.friends, screen_na'
        me = name, wait_on_rate_limit=True, count=200).pages():
            try:
                peeps.extend(page)
            except tweepy.TweepError as ex:
                print("Going to sleep:", ex)
                time.sleep(180)        
        final_peeps.extend(peeps)
    print(final_peeps)
    return final_peeps
```

These 2 functions allowed me to get not only the information about who each artist's followers were, but also who the followers were additionally following. Some cleaning was required beforehand in order to extrapolate correlations about the locations of these users, their relative age, etc. 


{{< figure src="https://lh3.googleusercontent.com/UPApTDGjmJz2jWSRnJXLtkOiL_t_n1G80K8dNSMtd5NifM2N7SRvKnFU_9S5jHDyUQh_mRQBvqAXAzTAvTjL1KbvW-wVHU7ftN58xBlIqW3fJsz1SjaGgzRduUn_TioSe2pvlPBFkdcLVNVrY6qgEwKSiUsRxEbCzhHBAFikVv1v12qeudC64gAb-FikELzGRiMRYWvqYiFccbxlfIsNqwggPQ7-Fwt34Fguc3fx6_5vhmED-Diq_IDqWjMJEtNCNDOcWW9R4WNgZDukUkppGCXm4LTdJ3AmP7Jq2D0_eeUJrmP2zH8ZPoqJHARyfRFti7fgP-EQ9DQytVtWCSkePNe_Z1KMEXjmPrKEZ19jPmget85GCw59Nq1N5AODJ5arBBSVFgHElb01yMmF88UKmRPzg4GQ9GZAbmiziykhZrO_1PUOisZr7gc6EZgnKo909QnlgC7BEiN_PQKwyN5V9b0jbAANnsJHWK_kF97H63M1mzT1yF1fETD3zJ0lHglkOviN_E4LjUCRTrDCinwwG3lWcj7DrbMF6s-Z3oSGJt9RL1H22DjOVvayfVXpqAvGSyhzV3gEbd5jzx_qJjh76N4v-HP_i9uxtP0e9HE8zVeFiCrtpsGeaejVIChjw3ngddimXV0Iucov2OpPa_xHI2R4mV7PvIcrelIC4fPnBjfhwOE1xHUcWnvuhecprw=w974-h495-no?authuser=0" title="Cleaned Follower Data" >}} 




After having done this for all 4 artists I began to run a series of mathematical and statistical tests in order to determine whether or not there were actual commonalities between all 4 artists followers.


## Mathematical/Statistical Modeling

I began by running multinomial regression models on each of the 4 artists followers to see if there were any shared characteristics that were statistically significant, but due to the sheer amount of categorical variables being tested between all of these users, there was no conclusive proof based on this model that there were any commonalities between the users. 

Given the fact that these 4 artists all had multiple collaborations with each other, I didn't think that the results of the multionomial regression model gave the full truth about the commonalities of all 4 artists' followers. In order to test this hypothesis, I ran a frequency table on this set of followers, and the results of that showed a completely different result:


{{< figure src = "https://lh3.googleusercontent.com/cAL4dGF7VuHKWZGSeK872jpdgn_lszQcNC2pNAS1x_1LNSFNniGONkYLfVdIhBP0RIVRnUdUwD-MF6Gn49qVubig0nwRypRCsJyykIHyl5vnGMHQTFdBaxmXyhySnTneReJo5PQzbOZCEgdw8LgZE0pDyGqFzcGQUMOBpjX55ju8Govi3vfp5qa4J5N5SWtNXuEYTEPFRsZSFG94tWSSEQ1qcQ0D_ZMzD7VJd4RiRQoRY-CDXNoriL1StcVBrfn-1KYiz9HipbMGPWWf8wEchsDmB3KGv39i-Y5mWEobgd0EBPOPgOxIgfTqiABupsXxWfbZEw-CjxuciCItqZye28gdQEMGqYfUMjq2XyIGslpqwZOlxFfnihowx8Y7BHm1q4mFuVG3alp0orkMWP05ipc_CZZmUOeuIcgqY_WOrecyCQJELKXeleZGMrfW6cIDgRxC2g5ifIqrMNVbRvUrmjFUUmNkLsWMLzYhLqoSO72FIG-1B5ZqBfWJrGO_QFroDLI8YmlEMq2ZOL4b7jAVXfF5jQGIAG4G7tzeZfUVSpQ7VlDtrhEuV8C4WChI9WG-RdJMfiLF5IAdIsDUXt70UDIN1ZqKKXWZ9Ks8HMVTOVCfsd9aLVbWUUJ-vXCal2X6Mc5bS-Vu5DRBJFgwN--MAzhWp5WoTnzYhl9uPp8ecgK6h26kGDeHXe5J6BSw7quix_d1clM=s974-w974-h670-no?authuser=0" title = "Follower Frequency Table" >}}

By viewing the data this way, it was easily able to identify that solely based on location, there definitely existed commanilities between all 4 artists' followers.

This same process was repeated to see if there were commonalities in who the followers of these 4 artists were additionally following:

{{< figure src = "https://lh3.googleusercontent.com/PHun_bZWYWoEX8xCfGcwsQLq5nV2jlEggGCsxWpfK2TYF4cxUI4zZWglDjIrHQ63268Ppwe0ChSCjYNmJtEQen3PErPLG_12U3C2UUjSvqDlWTuIwpzeyRDfEwMBFF0OP6w_Uyuxli5Gy9BB4q_lmjnH88IvNj91dF-LYV3ze65UkRp3s31lBU3oS0kDiwj0sQtcgSxKJo9Ry3FZU8y7WK-wCnoHqrpd0vvRNjZ3-Rk7XDTu4N1ePKT9vQ8-a2vOk-1VZnUaXbr_G01_Q1JKGw5aznlv4jzcIjMuLWps3ulk5WpTMUqiUSGoXAOn1K2CkhHV30B81kHs5yc8ZPSaLvfuJzPu0C6DlZZjhvnsECaSZE2wFLkr3Beq6zCAjGyS7QZpWY4DrPfvHzo3YII9ZFSEzedK73j2fMY9XgKKJ7PRGhNgoULr1mxOSBRdayK3fzCccByyv_8crigBnoEYOF6djfUz2nCAmT5J8IQlVaw3pGV0Bv7FYneIbj7dti0403o1zD2jgCesjApEjnSAdfQMLO0kimWiBXZovK2Ksl94H49voV1C3ocfQLPTEWwSq-h8hTfZCc12f3daz57WJrP7g380AL9gpnzkZ558NgoxFyO_bx9kNXL4OrbCbmjAaT5cEKpW4zhhnNkSXRKOrlUjuiLOLkNddTPdudvDe-nh845-35V0KRVOPZYG3Q=w385-h656-no?authuser=0" title = "Followed Frequency Table" >}}

Again, the frequency table showed that there were a large number of these 4 artists' followers who were similarily following other twitter accounts.


### What does this all mean?
The results from this venture showed that commonalities did in fact exist between all 4 artists' followers, which is important as it allows us to create a common user profile to appeal to in order to better promote these artists. 

### Future Steps

In order to build on the progress here, a future step would be to group the followers of these 4 artists by their general location(i.e. Regions of the USA, Major Continents, etc.), and then attempting to see if correlations exist between this set of followers based on that. I also plan on creating an efficient graph database to better track the connections between all of these users, even to see if there are pockets of these followers that follow each other.
