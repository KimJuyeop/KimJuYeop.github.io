# 파이썬에서 *args , **kwargs 는 무엇일까?

# *args 는 *arguments 의 줄임말이니 꼭 저 단어를 사용할 필요는 없다.

# * a라고 써도되고 , *b라도 써도된다.

# 이 지시어는 여러개의 인자를 함수로 받고자할때 사용한다.

# 예시


```python
def arg(*args):
    print(f"len of args:{len(args)}")
    for item in args:
        print(item)
```


```python
arg()
```

    len of args:0
    


```python
arg("arg1")
```

    len of args:1
    arg1
    


```python
arg("arg1","arg2")
```

    len of args:2
    arg1
    arg2
    


```python
def love_fruit(*Fruits):
    for fruit in Fruits:
        print(fruit[0], fruit[1:2], end= '')    
    print(type(Fruits), Fruits)
        
love_fruit('딸기')
love_fruit('딸기','포도')
love_fruit('딸기','포도','사과')
love_fruit("딸기","포도","사과","수박")
```

    딸 기<class 'tuple'> ('딸기',)
    딸 기포 도<class 'tuple'> ('딸기', '포도')
    딸 기포 도사 과<class 'tuple'> ('딸기', '포도', '사과')
    딸 기포 도사 과수 박<class 'tuple'> ('딸기', '포도', '사과', '수박')
    

# love_fruist 함수에서는 인자값을 *Fruits 으로 받는다

# 다른 단어로 바뀌어도 상관없이 동작한다

# 출력을 해보면 ' tuple'(튜플) 형태임을 알 수 있다

# 여러개의 인자를 함수로 호출하면 내부에서는 튜블로 인식한다

# =================================================


# ** kwargs는 (키워드 = 특정값) 형태로 호출할 수 있다

# 그것은 그대로 딕셔너리 형태로 {'키워드':'특정 값'} 함수 내부로 전달

# 예시



```python
def kwarg(**kwargs):
    print(f"len of kwargs:{len(kwargs)}")
    for key, value in kwargs.items():
        print(f"key:{key}, value:{value}")
```


```python
kwarg()
```

    len of kwargs:0
    


```python
kwarg(arg1 = "good")
```

    len of kwargs:1
    key:arg1, value:good
    


```python
kwarg(arg1="good",arg2="bad")
```

    len of kwargs:2
    key:arg1, value:good
    key:arg2, value:bad
    


```python
def introduceEnglishName(**kwargs):
    for key,value in kwargs.items():
        if 'ant' in kwargs.keys():
            print("주인님 오셨군요. 오늘 기분이 어떠세요?")
        else: print("{0}is{1}".format(key, value))    
```


```python
introduceEnglishName(name="chris!!")
introduceEnglishName(ant="david!!")
```

    nameischris!!
    주인님 오셨군요. 오늘 기분이 어떠세요?
    


```python
def blog_printer1(*blogs):
    for post in blogs:
        print(post)
        
블로그1 = '첫번째 만듬'
블로그2 = '성공해서 두번째 블로그도 만듬'
블로그3 = '세번째도 만듬'
```


```python
blog_printer(블로그1, 블로그2, 블로그3)
```

    첫번째 만듬
    성공해서 두번째 블로그도 만듬
    세번째도 만듬
    

#  *args 사용법은 순서도 중요하다 

#  * args 말고도 변수를 하나 더 매개 변수로 추가해 보고 순서를 바꿔보기


```python
def blog_printer(name, *blogs):
    print(name)
    for post in blogs:
        print(post)
        
admin = 'admin'
blog1 = "first blog"
blog2 = 'second blog'
blog3 = 'third blog'

blog_printer(admin, blog1, blog2, blog3)
```

    admin
    first blog
    second blog
    third blog
    


```python
def blog_printer(*name, blogs):
    print(name)
    for post in blogs:
        print(post)
admin = 'admin'
blog1 = "first blog"
blog2 = 'second blog'
blog3 = 'third blog'        
blog_printer(admin, blog1, blog2, blog3)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-203-f7329b75448f> in <module>
          7 blog2 = 'second blog'
          8 blog3 = 'third blog'
    ----> 9 blog_printer(admin, blog1, blog2, blog3)
    

    TypeError: blog_printer() missing 1 required keyword-only argument: 'blogs'


# args는 일반 변수보다는 뒤에 위치해 있어야 한다

# 파이썬은 어디서부터 어디까지를 * 변수에 담을지 알 수 없다

# 그래서 맨 앞에 특정 변수를 명시해두고, 그 뒤에는 *args 를 넣어줘야한다.

# * args 와 , **kwargs를 둘 다 사용해보기


```python
def blog_printer(name, *blogs, **blog_benefits):
    '''
    names: 블로그 주인 이름
    *blogs : 블로그를 만들 때 설명
    **blog_benefits: 블로그 수익
    '''
    print(name)
    for post in blogs:
        print(post)
    for blog, benefits in blog_benefits.items():
         print(blog, "수익은>>", benefits)
         
admin = 'admin'
blog1 = "first blog"
blog2 = 'second blog'
blog3 = 'third blog'

help(blog_printer)
blog_printer(admin, blog1, blog2, blog3, blog_benefits1= 100, blog_benefits2 = 50, blog_benefits3 = 30)
```

    Help on function blog_printer in module __main__:
    
    blog_printer(name, *blogs, **blog_benefits)
        names: 블로그 주인 이름
        *blogs : 블로그를 만들 때 설명
        **blog_benefits: 블로그 수익
    
    admin
    first blog
    second blog
    third blog
    blog_benefits1 수익은>> 100
    blog_benefits2 수익은>> 50
    blog_benefits3 수익은>> 30
    

# 순서를 바꾸면 어떻게 될까?


```python
def blog_printer(name,**blog_benefits, *blogs):
    '''
    names: 블로그 주인 이름
    *blogs : 블로그를 만들 때 설명
    **blog_benefits: 블로그 수익
    '''
    print(name)
    for post in blogs:
        print(post)
    for blog, benefits in blog_benefits.items():
         print(blog, "수익은>>", benefits)
         
admin = 'admin'
blog1 = "first blog"
blog2 = 'second blog'
blog3 = 'third blog'

help(blog_printer)
blog_printer(admin, blog1, blog2, blog3, blog_benefits1= 100, blog_benefits2 = 50, blog_benefits3 = 30)
```


      File "<ipython-input-205-8418625d1888>", line 1
        def blog_printer(name,**blog_benefits, *blogs):
                                               ^
    SyntaxError: invalid syntax
    


 # 작동하지 않는다
 
 # 이를 통해서 *args, **kwargs 도 순서가 있다는것을 확인 할 수 있다.
 
 
# *변수 -> 여러개가 아규먼트로 들어올때, 함수 내부에서는 해당 변수를 '튜플'로 처리
# **변수 -> 키워드= " 러 입력할 경우에 그것을 각각 키와 값으로 가져오는 '딕셔너리'로 처리


<br>
<br>

참고 : https://brunch.co.kr/@princox/180#comment