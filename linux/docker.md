# docker
## docker日志查询
* docker logs -f -t --tail 100 containerId
* docker logs -f -t --since="2018-02-08" --tail=100 containerId 查看指定时间后的日志，只显示最后100行
* docker logs -f -t --since 30m containerId 查看最近30分钟的日志
* docker logs -t --since="2018-02-08T13:23:37" --"2018-01-08T13:23:37" containerId 查看某个时间段的日志
