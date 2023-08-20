# Python-35-
Python学习笔记(35)
# p129 文件读写的原理_读取磁盘文件中的内容
#从别的地方到达内存当中称为读，从内存往外面输出叫做写
#语法规则:  file=open(filename[,mode,encoding])
#file为被创建的文件对象  open为创建文件对象的函数  filename为要创建或打开的文件名称  mode为打开模式默认为只读  encoding为默认文本文件中字符的编写格式为gbk
file=open('a.txt','r')
print(file.readlines())  #readlines会读取文件当中的所有内容
file.close()



# p130 常用的文件打开模式
file=open('b.txt','w')
file.write('helloworld')
file.close()  #磁盘上没有文件则进行创建，如果有文件则完成内容的替换

file=open('b.txt','a')  #文件以追加模式打开文件，若果文件不存在则创建文件，文件指针在文件开头，如果文件存在，则在文件末尾追加内容，文件指针在原文件末尾
file.write('helloworld')
file.close() 

src_file=open('logo.png','rb')
targe_file=open('copylogo.png','wb')
print(target_file.write(src_file.read))
target_file.close()
src_file.close()  #b以二进制打开文件，不能单独使用，需要与其他模式一起使用，rb或wb

#+以读写的方式打开文件，不能单独使用，需要与其他模式一起使用,a+



# p131 文件对象的常用方法
file=open('a.txt','r')
print(file.read())  #从头读到尾
#read函数里面可以写数字来打印想要的字符数
print(file.readline())  #从文本中读取一行内容
print(file.readlines())  #输出的是一个列表，把每一行的内容都打印出来了

file=open('c.txt','a')
file.write('hello')
lst=['java','go','python']  #不仅可以打印字符串，还可以打印列表
file.writelines(lst)
file.close()

file=open('a.txt','r')
file.seek(2)  #这里有个中文两个字节，如果想跳过中文则需要输出2，seek(2)是将文件的指针指向第三个字节
print(file.read())
print(file.tell())  #tell()函数是告诉你文件指针指向的字节数
file.close()

file=open('d.txt','a')
file.write('hello')
file.flush()
file.write('world')
file.close()  #输出helloworld，flush把缓冲区的内容写入文件，但不关闭文件



# p132 with语句
with open('a.txt','r') as file:
    print(file.read())

#MyContentMgr实现了特殊方法__enter__(),__exit__()称为该类对象遵守了上下文管理器协议，该类对象的实例对象，称为上下文管理器
#MyContentMgr()创建的1实例对象就称为上下文管理器
class MyContentMgr(object):
    def __enter__(self):
        print('enter方法被调用执行了')
        return self

    def __exit__(self,exc_type,exc_val,exc_tb):
        print('exit方法被调用执行了')

    def show(self):
        print('show方法被调用执行了')

with MyContentMgr() as file:  #相当于file=MyContentMgr()
    file.show()  #这里三个方法都被输出执行了

with open('logo.png','rb') as src_file:
    with open('copy2logo.png','wb') as target_file:
        target_file.write(src_file.read())  #目标文件读了什么写什么



# p133 os模块的常用函数
#os模块是与操作系统相关的一个模块
import os
os.system('notepad.exe')
os.system('calc.exe')
#直接调用可执行文件
os.startfile('文件磁盘地址')

import os
print(os.getcwd())

lst=os.listdir('chap15')
print(lst)

os.mkdir('newdir2')
os.makedirs('A/B/C')  #创建多级目录

os.rmdir('newdir2')  #删除目录

os.removedirs('A/B/C')  #移除多级目录

os.chdir('E:\\vippython\\chap14')  #将path设置为当前目录
print(os.getcwd())



# p134 os.path模块常见方法_课堂案例
import os.path
print(os.path.abspath('demo13.py'))  #用于获取文件或目录的绝对路径
print(os.path.exsists('demo13.py')os.path.exists('demo18.py'))  #用于判断文件或目录是否存在，如果存在返回True，否则返回False
print(os.path.join('E:\\Python','demo13.py'))  #输出E:\Python\demo13.py 将目录与目录或者文件名拼接起来
print(os.path.split('E:\\vipython\\chap15\\dmeo13.py'))  #这里将文件的路径和文件的名称进行了拆分
print(os.path.splitext('demo13.py'))  #把文件的名字和文件的·后缀进行了拆分
print(os.path.basename('E:\\vippython\\chap15\\demo13.py'))  #将文件的名字提取出来输出demo13.py
print(os.path.dirname('E:\\vippython\\chap15\\demo13.py'))  #这里将目录提取出来
print(os.path.isdir('E:\\vippython\\chap15\\demo13.py'))  #这里输出False，因为这里是文件不是目录

import os
path=os.getcwd()
lst=os.listdir(path)
for filename in lst:
    if filename.endwith('.py')
        print(filename)  #获取指定目录下的所有python文件

import os
path=os.getcwd()
lst_files=os.walk(path)
for dirpath,dirname,filename in lst_files:
    print(dirpath)
    print(dirname)
    print(filename)
