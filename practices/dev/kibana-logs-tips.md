# Kibana Logs Tips

## Log Search
### Save Search
You can create and save search queries for your application in all environments and then use them to open your logs quickly. 
1. Use menu Discover on the left, pick index from drop-down which corresponds to the needed environment 
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/pick_environment.png)
2. Select docker image name with your application
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/select_docker_name.png)
3. Save search with proper name
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/save_search.png)
### Pre-Saved Searches
It is easy to use pre-saved search queries to see some logs 
![Open Search](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/open_search.png)
### Quick Time Range 
You can change time range for search
![Quick Time Range](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/quick_time_range.png)
### Absolute Time Range
Absolute time range can help to search logs in particular time range
![Absolute Time Range](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/absolute_time_range.png)
### Search by content
Simplest search query to find an exact match in logs. Can be a good starting point.
![Search by content](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/search_by_content.png)
### Surrounding Messages
Kibana provides ability to open surrounding messages around some message which you found.
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/surrounding_messages.png)
You can show as many lines before and after message as you need to understand the context of log message
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/surrounding_messages_1.png)

## Log view
Regular log view can be too messy 
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/regular_log_view.png)
To improve log readability you can use message as key part of log to eliminate other log elements which create noise
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/message_view.png)
As a result, logs will be more readable
![](https://github.com/ca-cwds/development-practices/blob/master/images/kibana/message_view_1.png)
