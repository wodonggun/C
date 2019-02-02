# 2차원 배열 주소 
```
char arr[5][2] = { {0,1},{2,3},{4,5},{6,7},{8,9} };

int main()
{

	printf("%d\n", &arr);
	printf("%d\n", &arr + 1);

	printf("%d\n", arr);

	printf("%d\n", &arr[0] + 1);
}
```

- `&arr + 1` = arr 변수의 크기는 5x2 10바이트이므로 arr주소+10의 주소가 출력됨.
- `&arr[0] + 1`  = arr[0]의 변수의 크기는 2이므로 `arr[1](=arr[1][0])`의 주소를 나타낸다. 

- `arr과 &arr의 차이` : arr은 배열, &arr은 주소를 나타내지만 포인터가 아니기 때문에 `*(&arr[0]+1)`를 출력하여도 똑같이 주소가 출력됨.


# 함수 포인터

- 함수 포인터를 장점
1. 포인터 배열을 통해서 여러개의 함수 주소를 가지고있는 배열을 만들 수 있다.
2. 구조체 안에 다른 멤버변수와 함수 포인터를 넣을 수 있다. 
3. 함수 포인터를 매개변수나 반환값으로 보낼 수 있다. 
![img](https://dojang.io/pluginfile.php/655/mod_page/content/17/unit68-1.png)


```
#include <stdio.h>

void hello()     // 반환값과 매개변수가 없음
{
	printf("Hello, world!\n");

}

void bonjour()    // 반환값과 매개변수가 없음
{
	printf("Hello, Git!\n");
}

int Check(int a)
{
	if (a == 0)
		return 1;
	else
		return 0;
		
}

int main()
{
	void(*fp)();   // 반환형(*변수명)(매개변수void) 
		

	fp = hello;     // hello 함수의 메모리 주소를 함수 포인터 fp에 저장
	fp();           // 함수 호출

	fp = bonjour;   // 함수 포인터의 호출 함수 변경
	fp();           // 바뀐 함수 호출



	int(*ch)(int);	//int 반환형의 ch포인터함수,매개변수는 int형 선언 

	ch = Check;    // 함수포인터에 Check함수 대입

	printf("%d", ch(10));

	return 0;
}

```


# 매개변수, 리턴타입을 
```
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int add(int a, int b)    // int형 반환값, int형 매개변수 두 개
{
	return a + b;
}


int(*getAdd_())(int, int) // 함수 포인터 반환, int형 매개변수 두 개
{
	return add;
}

int(*getAdd(int x, int y))(int, int)   // 함수 포인터 반환, int형 매개변수 두 개
{
	printf("%d %d\n", x, y);    // x, y는 getAdd 함수의 매개변수
	return add;
}



int main()
{

	printf("%d\n", getAdd_()(10, 20));

	printf("%d\n", getAdd(8, 9)(10, 20));    // 8, 9는 getAdd에 전달
											 // 10, 20은 getAdd에서 반환된 add에 전달

	printf("%d\n", add(10, 20));

	return 0;
}
```

# 함수 포인터 배열

```
int (*fp[4])(int, int);

for(int i=0;i<4;i++)
{
 fp[i](30,50);
}

```



# 심볼테이블

int num이라고 선언을 하지만 컴퓨터가 num이란 변수를 이해할 수 없다.<br>
따라서 num이란 변수의 타입과 값이 저장된 주소를 매핑하여 테이블로 가지고 있어야 한다.<br>

![img](https://t1.daumcdn.net/cfile/tistory/153961354D9D78CD2D) <br>

컴파일러가 생성되면서 같이 생성되고, 컴파일 종료시에 같이 소멸됨. <br>


# 함수의 변수 저장 위치
`힙 영역`에는 동적변수  (런타임 시점에서 결정)
`스택 영역`에는 지역변수,매개변수 (컴파일 시점에서 결정)
`데이터 영역`에는 전역변수와 Static변수
`코드 영역`에는 소스코드가 저장됨.

## 컴파일 시점과 런타임 시점

- 비정상적인 배열 선언
`지역변수는 컴파일 시점에서 생성되는데 컴파일러는 arr이 int형인건 알지만 크기는 알수 없다.(scanf에서 받아야 알 수 있음)`
```
int main()
{ 
	i = 0; 	
	
	scanf("%d", &i); 
	
	int arr[i];
	
  return 0;
}

```



- 그럼 이건 왜 안되는가?
`컴파일 시점에서는 int i라는 선언만 인식하고, i = 10이라는 초기화 값은 런타임 시점에서 결정된다`

```
int main() {

	int i = 10; 
	int arr[i];
	
  return 0; 
}
```

그래서 `힙 영역`은 프로그램이 실행되는 동안(런타임)에 결정되야 할때 사용된다.


# malloc, calloc, realloc
malloc은 void 리턴타입의 주소를 반환(쓰레기값 저장되어있음) `malloc(5*sizeof(int))` <br>
calloc은 malloc과 똑같지만 함수호출방식이 조금다르고, 메모리는 0으로 초기화 시켜줌 `calloc(5,sizeof(int))` <br>
realloc 메모리의 크기를 변화시킬때 사용 <br>



	

