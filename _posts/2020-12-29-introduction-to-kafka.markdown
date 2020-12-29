---
layout: post
title:  "Running Kafka Service on Windows"
date:   2020-12-29 15:24:46 +0530
categories:
---

Steps to install Kafka:

cd C:\Users\SIDDHESH\Desktop\kafka\bin\windows


Download binary file, not source file. Extract it, and rename folder to `kafka`, otherwise it will give errors.

In the main folder, create a  `data` folder. Inside that, create a `kafka` and `zookeeper` folder.

First, copy path address of `zookeeper` folder as text. Go into the `config` folder in the main folder, search for `zookeeper.properties` file. Search for `dataDir` and paste the copied path address. Make sure to replace '\' with '/'.

Now, copy path address of `kafka` folder as text. Go into the `config` folder in the main folder, search for `server.properties` file. Search for `logs.Dir` and paste the copied path address. Make sure to replace '\' with '/'. Also replace the `zookeeper.connect` property as `0.0.0.0:2181`.


Now open command window, and run the following command (make sure we are in the `kafka\bin\windows directory`):

{% highlight ruby %}
zookeeper-server-start.bat ../../config/zookeeper.properties
{% endhighlight %}

../../ -> indicates go 2 levels up from the current directory.



Open another command window, and run the following command:

{% highlight ruby %}
kafka-server-start.bat ../../config/server.properties
{% endhighlight %}


Create a topic:

{% highlight ruby %}
kafka-topics.bat --zookeeper 0.0.0.0:2181 --topic test_topic --create --partitions 1 --replication-factor 1
kafka-topics.bat --zookeeper 0.0.0.0:2181 --topic test_topic --describe
kafka-console-producer.bat --broker-list localhost:9092 --topic test_topic
{% endhighlight %}

This is the producer.
After the last line, we can type in messages, hit ENTER.


Now type in this:

{% highlight ruby %}
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test_topic --from-beginning
{% end highlight %}

This is the consumer.


Hopefully it's done!