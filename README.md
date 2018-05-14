# ScalaTest FeatureSpec acceptance test example

### Resources
ScalaTest FeatureSpec  
http://www.scalatest.org/getting_started_with_feature_spec

Scala HTTP client  
https://github.com/playframework/play-ws

## Prerequisites ##
Install Scala and sbt

## Test case ##
Acceptance test of for fetching a single video from Klaras REST API:   
 
<b>Given</b> there is a video added to ElasticSearch with id 'dn.screen9.1uwHxJLDuuBKBHGHQcissw'  
<b>When</b> fetching a video with id 'dn.screen9.1uwHxJLDuuBKBHGHQcissw'  
<b>Then</b> response should contain the right json body  

```json
{
  "id" : "dn.screen9.1uwHxJLDuuBKBHGHQcissw",
  "fileName" : "20171107-arbogany-1053_NormalHires.mp4",
  "title" : "Grafikfilm: Arbogamorden  (uppdaterad för hovrätten)",
  "description" : "Huvudpersonerna och händelserna som ledde fram till rättegången och dom mot den 42:åriga kvinnan och hennes pojkvän. Nu prövas målet i Svea Hovrätt",
  "streamUrl" : "https://video-cdn.dn.se/M/V/1/u/1uwHxJLDuuBKBHGHQcissw_360p_h264h.mp4?v=1&token=0ed558211ccafe3db4784",
  "thumbnails" : {
    "small" : "https://csp.screen9.com/img/1/u/w/H/thumb_1uwHxJLDuuBKBHGHQcissw/8.jpg",
    "large" : "https://csp.screen9.com/img/1/u/w/H/image_1uwHxJLDuuBKBHGHQcissw/8.jpg"
  },
  "duration" : "PT1M36.28S",
  "publishedAt" : null,
  "createdAt" : "2017-11-07T14:36:46.000+01:00",
  "createdBy" : null,
  "transcodeStatus" : "done",
  "sentToTranscodeAt" : "2017-11-07T14:38:12.000+01:00",
  "status" : "published"
}
```

## Setup test fixture ##
In nav project comment out existing Groovy tests mvn execution in script `.run.sh`, and then it to start containers with ElasticSearch, Redis and nav-klara-dx up and running:
```sh
./integration-test/nav-klara-it/run.sh
```

## Run test with sbt ##
```sh
sbt> testOnly example.NavKlaraVideoSpecAsync 
```

## Run test with IntelliJ ##
Right click on test an choose run

## Test Success Output
```sh
[info] NavKlaraVideoSpecAsync:
[info] Feature: Videos
[info] - Scenario: Fetch a single video
[info]   + Given there is a video added to elasticsearch
[info]   + When fetching a video with id dn.screen9.1uwHxJLDuuBKBHGHQcissw from nav-klara-dn
[info]   + Then response should contain the right data
[info] Run completed in 1 second, 514 milliseconds.
[info] Total number of tests run: 1
[info] Suites: completed 1, aborted 0
[info] Tests: succeeded 1, failed 0, canceled 0, ignored 0, pending 0
[info] All tests passed.
```

## Test Failure Outout
```sh
[info] NavKlaraVideoSpecAsync:
[info] Feature: Videos
[info] - Scenario: Fetch a single video *** FAILED ***
[info]   404 did not equal 200 (NavKlaraVideoSpecAsync.scala:47)
[info]   + Given there is a video added to elasticsearch
[info]   + When fetching a video with id dn.screen9.1uwHxJLDuuBKBHGHQcissw from nav-klara-dn
[info]   + Then response should contain the right data
[info] Run completed in 1 second, 654 milliseconds.
[info] Total number of tests run: 1
[info] Suites: completed 1, aborted 0
[info] Tests: succeeded 0, failed 1, canceled 0, ignored 0, pending 0
[info] *** 1 TEST FAILED ***
[error] Failed tests:
[error] 	example.NavKlaraVideoSpecAsync
[error] (Test / test) sbt.TestsFailedException: Tests unsuccessful
[error] Total time: 3 s, completed May 14, 2018 2:56:29 PM
```

### Pros
+ Can be run by IntelliJ
+ \<Click to se difference> in IntelliJ works
+ Nice output
 
### Cons
