首先是在tensorflow中输出相应的log，然后再启动tensorboard来查看对应的log中信息：tensorboard --logdir=run1:/tmp/mnist/1,run2:/tmp/mnist/2 --port=6006

—-logdir为读取相应的log然后展示起来，注意可以读入多个log来做对比
