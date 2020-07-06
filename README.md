from functools import wraps



def auth(db_type):
    def deco(func):
        @wraps(func)
        def warpper(*args,**kwargs):
            """
            这里是我的doc文件 warpper
            :param args:
            :param kwargs:
            :return:
            """
            res=func(*args,**kwargs)
            name=input("请输入您的名字：").strip()
            pwd=input("请输入您的密码：").strip()
            if db_type == "file":
                print("来源于文件验证")
                if name == "liuqi" and pwd == "123":
                    print("登录成功")
                else:
                    print("name or pwd error!")
            elif db_type == "mysql":
                print("来源于mysql数据库")
                if name == "liuqi" and pwd == "123":
                    print("登录成功")
                else:
                    print("name or pwd error!")
            elif db_type == "xldap":
                print("来源于xldap")
                if name == "liuqi" and pwd == "123":
                    print("登录成功")
                else:
                    print("name or pwd error!")
            return res
        return warpper
    return deco


@auth(db_type="xldap")
def index(name):
    '''
    这里是doc文件
    :param name:
    :return:
    '''
    print("这是在测试有参装饰器，%s请知晓" %(name))

index('梅梅')
print(index.__name__)
print(index.__doc__)
