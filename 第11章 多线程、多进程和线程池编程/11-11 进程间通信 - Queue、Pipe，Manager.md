```
import time
from multiprocessing import Process,Queue,Pool,Manager,Pipe
# from queue import  Queue #多进程编程中 这个queue不能使用
'''分隔符'''
# def producer(queue):
#     queue.put("a")
#     time.sleep(2)

# def consumer(queue):
#     time.sleep(2)
#     data = queue.get()
#     print(data)

# if __name__ == "__main__":
#     queue = Queue(10)
#     my_producer = Process(target=producer,args=(queue,))
#     my_consumer = Process(target=consumer,args=(queue,))
#     my_producer.start()
#     my_consumer.start()
#     my_producer.join()
#     my_consumer.join()
'''分隔符'''
#共享全局变量通信
#共享全局变量不能适用于多线程编程，可以适用于多线程，数据隔离

# def producer(a):
#     a+=1
#     time.sleep(2)

# def consumer(a):

#     time.sleep(2)
#     print(a)

# if __name__ == "__main__":
#     a = 1
#     my_producer = Process(target=producer,args=(a,))
#     my_consumer = Process(target=consumer,args=(a,))
#     my_producer.start()
#     my_consumer.start()
#     my_producer.join()
#     my_consumer.join()

# multiprocessing 中的queue不能用于pool进程池
#pool中的进程间通信需要使用manager中的queue
#需要对manager进行实例化的queue ：Manager().Queue()

# def producer(queue):
#     queue.put("a")
#     time.sleep(2)

# def consumer(queue):
#     time.sleep(2)
#     data = queue.get()
#     print(data)

# if __name__ == "__main__":
#     queue = Manager().Queue(10)
#     pool =  Pool(2)
#     pool.apply_async(producer,args=(queue,))
#     pool.apply_async(consumer,args=(queue,))
#     pool.close()
#     pool.join()

#通过pipe管道 实现进程间通信
# def producer(pipe):
#     pipe.send("bobby")

# def consumer(pipe):
#     print(pipe.recv())

# if __name__ == "__main__":
#     recevie_pipe,send_pipe = Pipe()
#     #pipe只能适用于两个进程
#     my_producer=Process(target=producer, args=(send_pipe,))
#     my_consumer = Process(target=consumer, args=(recevie_pipe,))
#     my_producer.start()
#     my_consumer.start()
#     my_producer.join()
#     my_consumer.join()
'''分隔符'''
def add_data(p_dict,key,value):
    p_dict[key] = value

if __name__ =="__main__":
    progress_dict =Manager().dict()
    first_progress = Process(target=add_data,args=(progress_dict,"bobby1",22))
    second_progress =Process(target=add_data,args=(progress_dict,"bobby2",23))
    first_progress.start()
    second_progress.start()
    first_progress.join()
    second_progress.join()

    print(progress_dict)
