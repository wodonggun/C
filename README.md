# C
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
- '&arr[0] + 1` = arr[0]의 변수의 크기는 2이므로 `arr[1](=arr[1][0])`의 주소를 나타낸다. 

