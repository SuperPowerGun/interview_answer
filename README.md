# interview_answer
Linux应用：
1.已知某个进程的pid是6666,如何找到它当前打开了哪些文件？
lsof -p 6666
2.发现端口8001被占用，如何找出是哪个进程占用了该端口？
netstat -tunlp | grep 8001

3.假设有进程P持续向文件F写入数据，此时把文件F删除，进程P的写入会失败吗？磁盘占用是否会持续增加？为什么？
不会写入失败，会持续增加。有其他文件句柄占用时删除文件F相当于删除链接，而不是删除具体的数据。


数据处理：
MYSQL:
select * from table t1 where (select count(1) from table where name=t1.name and score >= t1.score) <=2;

Python:
def cal_remain_seconds(user_id):
    import time
    user_seconds_info = dict()
    day_2_seconds = 24 * 3600
    with open('orders.csv', 'r') as f:
        for i in f.readlines():
            i = i.replace('\n', '')
            i = i.split(',')
            uid, timestamp, days = map(int, i)
            end_timestamp = timestamp + days * day_2_seconds
            if uid not in user_seconds_info:
                user_seconds_info[uid] = end_timestamp
            else:
                if timestamp > user_seconds_info[uid]:
                    user_seconds_info[uid] = end_timestamp
                else:
                    user_seconds_info[uid] += days * day_2_seconds
    if user_id not in user_seconds_info:
        return 0
    remain_seconds = user_seconds_info[user_id] - int(time.time())
    return remain_seconds if remain_seconds > 0 else 0
 
