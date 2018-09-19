##this
-----------------

1. 전역공간에서
- window / global
- 콘솔에서 this

~~~javascript

console.log(this);

~~~

2. 함수내부에서
- window / global
- default 값이 window / global 이며 추후 변경될 수 있다.
- 함수는 전역객체의 메소드다.

3. 메소드 호출시
- 메소드 호출 주체
- ex) a.b, a.b.c

~~~javascript

function a (){
    console.log(this);
}

a();

var ten = 10;
var obj = {
    one : 1,
    a : function(){
        console.log(this.a);
        
        function z (){
            console.log(this.a);
        }
        z();
    }
    
};

obj.a();

~~~


- scope 체인을 이용한 우회

~~~javascript

var ten = 10;
var obj= {
    one : 1,
    a : function(){
        var self = this;
        console.log(this.a);
        
        function z (){
            console.log(self.a);
        }
        z();
    }
    
};

obj.a();

~~~

4. callback 에서
- 기본적으로는 함수내부에서와 동일
- 배경지식( call, apply, bind )

~~~javascript

function a (x,y,z){
    console.log(this, x, y, z);
}

var b = {
    c : 'eee',
};

// thisArg -> 이 인자를 this로 인식
// arg1 -> 인자
// 1. call (즉시호출)
<pre>
func.call(thisArg, arg1, arg2 , .... ,)
</pre>
a.call(b,1,2,3);


// 2. apply (즉시호출)
<pre>
func.apply(thisArg, [argsArray])
</pre>
a.apply(b,[1,2,3]);

// 3. bind (새로운 함수 생성)
<pre>
func.bind(thisArg, arg1, arg2 , .... ,)
</pre>
var c = a.bind(b);

c(1,2,3);

var d = a.bind(b,1,2);

d(3);

~~~

~~~javascript

var callback = function(){
    console.dir(this);
};

var obj = {
    a: 1,
    b: function(cb) {
        cb();
    }
};

obj.b(callback);

~~~

5. 생성자함수에서
- 인스턴스

~~~javascript


function Person(n, a){
    this.name = n;
    this.age = a;
}

var newPerson = new Person('kim', 10);
console.log(newPerson);

~~~


##클로저

---------------------------------------



- 함수와 그 함수가 선언될 당시의 환경정보의 조합.
- 최초 선언시의 정보를 유지.

1. 접근 권한 제어, 지역변수 보호
~~~javascript

function a(){
    var x = 1;
    function b() {
        console.log(x);
    }
    b();
}

a();
console.log(x);

~~~

2. 데이터 보존 및 활용

~~~javascript

function a(){
    var x = 1;
    return function b() {
        console.log(x);
    }
}

var c = a();
c();

~~~

- 스코트는 정의될때 생성.
- 1.png
- 2.png
- 3.png


프로토타입

