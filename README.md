# 데이터구조 코드를 올리는 연습장
---
**2023.04.12**
---
예제: 선형큐 프로그램
```
#include<stdio.h>						
#include<stdlib.h>
#define MAX_QUEUE_SIZE 5

typedef int element;
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

void error(char* message) {						// 오류가 났을때 문자열을 받아 받은 문자열을 출력하는 프로그램
	fprintf(stderr, "%s\n", message);
	exit(1);
}

void init_queue(QueueType* q) {						// 큐를 -1로 초기화 하는 함수
	q->rear = -1;
	q->front = -1;
}

void queue_print(QueueType* q) {					// 큐를 출력하는수함수
	for (int i = 0; i < MAX_QUEUE_SIZE; i++) {
		if (i <= q->front || i > q->rear) {
			printf(" | ");
		}
		else {
			printf("%d | ", q->data[i]);
		}
		
	}
	printf("\n");
}

int is_full(QueueType* q) {						// 큐가 포화상태인지 검사하는 함수
	if (q->rear == MAX_QUEUE_SIZE - 1) {
		return 1;
	}
	else {
		return 0;
	}
}

int is_empty(QueueType* q) {						// 큐가 공백상태인지 검사하는 함수
	if (q->front == q->rear) {
		return 1;
	}
	else {
		return 0;
	}
}

void enqueue(QueueType* q, int item) {					// 큐에 삽입하는수함수
	if (is_full(q)) {
		error("큐가 포화상태입니다.");
		return;
	}
	q->data[++(q->rear)] = item;
}

int dequeue(QueueType* q) {						// 큐에서 삭제하는 함수
	if (is_empty(q)) {
		error("큐가 공백상태입니다.");
		return -1;
	}
	int item = q->data[++(q->front)];
	return item;
}

int main(void) {
	int item = 0;
	QueueType q;							//큐 객체를 지정한다

	init_queue(&q);

	enqueue(&q, 10); queue_print(&q);				
	enqueue(&q, 20); queue_print(&q);
	enqueue(&q, 30); queue_print(&q);
	
	item = dequeue(&q); queue_print(&q);
	item = dequeue(&q); queue_print(&q);
	item = dequeue(&q); queue_print(&q);
	return 0;
}
```
