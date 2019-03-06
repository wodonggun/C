# 구조체 vector sorting 하기
```
#include <stdio.h>
#include <string>
#include <algorithm>
#include <vector>

using namespace std;

struct test {
	string a;
	int b;
};

bool cmp(const test& a, const test& b)
{

	return a.b < b.b;
}


int main()
{
	vector<test> vec;

	vec.push_back({ "asd",4 });
	vec.push_back({ "zzz",2 });
	vec.push_back({ "aaa",3 });
	vec.push_back({ "bbb",1 });


	sort(vec.begin(), vec.end(), cmp);


	return 0;
}
```
